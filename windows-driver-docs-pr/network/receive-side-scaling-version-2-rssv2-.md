---
title: 接收端缩放版本 2 (RSSv2)
description: 本主题介绍了接收端缩放版本 2 (RSSv2)
ms.assetid: 192CAA41-0D17-4C06-8F13-68EA7C26D023
keywords: 接收方缩放版本 2、 RSSv2、 接收端缩放版本 2 WDK，RSSv2 网络驱动程序
ms.date: 10/12/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7dad30280a68c572c982e119b16bbce0b8293d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353212"
---
# <a name="receive-side-scaling-version-2-rssv2"></a>接收端缩放版本 2 (RSSv2)

[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

[接收方缩放](ndis-receive-side-scaling2.md)提高了与多处理器系统上的网络数据处理相关的系统性能。 NDIS 高 6.80 英寸及更高版本支持 RSS 版本 2 (RSSv2) 通过提供动态的每个 VPort 进行传播的队列来扩展 RSS。

## <a name="overview"></a>概述

与 RSSv1 相比，RSSv2 缩短的 CPU 负载度量和更新间接表之间的时间。 这将在高流量的情况下避免缓慢。 若要实现此目的，RSSv2 执行其操作在 IRQL = DISPATCH_LEVEL，处理该请求的处理器上下文中，并仅对指向当前处理器的间接寻址表条目的子集。 这意味着，可以动态分散 RSSv2 比 RSSv1 更敏捷地接收多个处理器上的队列。

两个 Oid [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)并[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)，已在 RSSv2 微型端口驱动程序，设置适当的 RSS 功能和控件中引入间接寻址分别表。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 是正则 OID，而 OID_GEN_RSS_SET_INDIRECTION_ENTRIES 是不能返回 NDIS_STATUS_PENDING 同步 OID。 有关这些 Oid 的详细信息，请参阅其单个引用页。 有关同步的 Oid 的详细信息，请参阅[NDIS 6.80 中的同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

## <a name="rssv2-terminology"></a>RSSv2 术语

本主题使用以下术语：

| 术语 | 定义 |
| --- | --- |
| RSSv1 | 第一代接收端缩放机制。 使用[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)。 |
| RSSv2 | 第二个生成接收的方缩放机制支持 Windows 10，版本 1803年和更高版本，本主题中所述。 |
| 扩展实体| 微型端口适配器本身在本机 RSS 模式或在 RSSv2 模式下 VPort。 |
| ITE | 间接寻址表项 （项） 的给定缩放实体。 每个 VPort Ite 的总数不能超过**NumberOfIndirectionTableEntriesPerNonDefaultPFVPort**或**NumberOfIndirectionTableEntriesForDefaultVPort** VMQ 模式或本机 RSS 中的 128用例。 **NumberOfIndirectionTableEntriesPerNonDefaultPFVPort**并**NumberOfIndirectionTableEntriesForDefaultVPort**属于[NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。 |
| 缩放模式 | 每个 VPort vmswitch 策略，用于控制其 Ite 在运行时的处理方式。 这可以是静态 （由于负载发生变化而没有 ITE 移动） 或动态 （扩展和根据当前流量负载合并）。 |
| 队列 | 一个基础硬件的对象 （队列） 支持项。 具体取决于硬件和间接表配置队列可能返回多个 Ite。 总数目的队列，其中包括一个由默认的队列，不能超过通常由管理员设置的预配置的限制。 |
| 默认的处理器 | 一个处理器，它接收的数据包不能为其计算哈希值。 每个 VPort 具有默认处理器。
| 主处理器 | 指定为一个处理器**ProcessorAffinity**的成员[NDIS_NIC_SWITCH_VPORT_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451597) VPort 创建期间的结构。 此处理器可以更新在运行时，并指定 VMQ 流量定向的位置。 |
| 源 CPU | 当前映射到 ITE 处理器。 |
| 目标 CPU | 项被重新映射到 （使用 RSSv2） 处理器。 |
| 执行组件 CPU | 处理器的 RSSv2 提出请求。 |

## <a name="advertising-rssv2-capability-in-a-miniport-driver"></a>播发 RSSv2 微型端口驱动程序中的功能

微型端口驱动程序通过设置播发 RSSv2 支持**CapabilitiesFlags**的成员[NDIS_RECEIVE_SCALE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff567220)结构*NDIS_RSS_CAPS_SUPPORTS_INDEPENDENT_ENTRY_MOVE*标志。 此功能，才能 RSSv2 的 CPU 负载平衡功能，连同*NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED*使 RSSv1 动态均衡 VPorts （非默认的标志Vmq)。

> [!NOTE]
> 上层协议假定默认 VPort 主处理器，可以移动的 RSSv2 微型端口驱动程序。

如果微型端口适配器不播发 RSSv2 功能，所有已启用 VMQ 的 VPorts 保持静态分配模式，即使这些 VPorts 请求以执行动态分配。 RSS 参数的配置 RSSv1 OID [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)，用于这些 VPorts 仍处于静态分配模式。

只需实现一个 RSS 控制机制-RSSv1 或 RSSv2 微型端口驱动程序。 如果该驱动程序播发 RSSv2 支持，NDIS 将转换为 RSSv1 Oid RSSv2 Oid 如有必要为 congifure VPort 每个分布。 微型端口驱动程序必须支持两个新 Oid 和修改 RSSv1 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 的行为，如下所示：

- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)仅针对 RSSv2 中的查询请求，也不用于设置 RSS 参数。
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)是查询，而用于配置缩放实体的参数数目的队列，数 Ite，RSS 启用/禁用，例如设置 OID 和哈希处理关键更新。
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)方法 OID 用于执行修改的间接寻址表条目。

## <a name="handling-rssv2-oids"></a>处理 RSSv2 Oid

[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)仅用来查询给定缩放实体的当前 RSS 参数。 在 RSSv1，此 OID 用于设置参数。 支持 RSSv2 的微型端口驱动程序，请 NDIS 自动驱动程序执行此角色转换并发出以下两个 Oid 以设置参数而不是。

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)是正则 OID 和作为 RSSv1 中处理 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 处理相同。 NDIS 轻型筛选器驱动程序 (LWFs) 在 NDIS 6.80 之前看不到此 OID。

[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)，，但[同步 OID](synchronous-oid-request-interface-in-ndis-6-80.md) ，不能返回 NDIS_STATUS_PENDING。 必须执行并在发起 OID 的处理器上下文中完成此 OID。 如 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2，它还对不可见之前 NDIS 6.80 NDIS LWFs。 LWFs 在 NDIS 6.80 及更高版本不允许延迟此 OID 或将移动到另一个处理器。 其有效负载包含的数组的简单"移动项"操作，其中每个包含要将缩放实体的单个项移动到不同目标 CPU 的命令。 数组的元素可以引用不同的缩放实体 (VPorts)。

每种类型的 NDIS 驱动程序、 微型端口、 筛选和协议，具有入口点以支持同步 OID 请求接口：

| NDIS 驱动程序类型 | 同步 OID 处 | 要发起同步 Oid 函数 |
| --- | --- | --- |
| 微型端口 | [*MiniportSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-miniport_synchronous_oid_request) | 不可用 |
| Filter | <ul><li>[*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request)</li><li>[*FilterSynchronousOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request_complete)</li></ul> | [**NdisFSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsynchronousoidrequest) |
| 协议 | 不可用 | [**NdisSynchronousOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissynchronousoidrequest) |

## <a name="rss-state-transitions-ite-updates-and-primarydefault-processors"></a>RSS 状态转换、 ITE 更新和主/默认处理器

### <a name="steering-parameters"></a>控制参数

在 RSSv2，不同的参数用于控制流向正确 CPU 具体取决于 RSS 状态 （启用或禁用）。 当禁用 RSS 时，仅主处理器使用用于将流量定向。 当启用了 RSS 时，用于将流量定向使用默认的处理器和所有 Ite。 这些*控制参数*是 labele 为"活动"或"非活动"下, 表中总结：

| 控制参数 | 禁用 RSS | 启用 RSS |
| --- | --- | --- |
| 主处理器 | 活跃 | Inactive |
| 默认的处理器 | Inactive | 活跃 |
| ITE[0..N] | Inactive | 活跃 |

当控制参数处于*active*状态中时，会将流量定向。 从 RSS 的那一刻起状态会使参数的切换*处于非活动状态*，微型端口驱动程序必须向参数跟踪更改，直到反向转换再次激活。 这意味着，需要跟踪对默认处理器和间接表项的所有更新，RSS 禁用该扩展的实体时，微型端口驱动程序。 当启用了 RSS 时，默认的处理器和间接表的当前跟踪的状态应才会生效。

已启用软件 vRSS 时，例如，考虑此方案。 在这种情况下，间接表已存在于上层协议，服务器当前使用的较高层的软件进行传播的代码。 如果，在硬件 RSS 支持过程中，所有项也都开始指向之前的更新的主处理器*移动*间接表项是颁发给并执行的硬件，可能会遇到主处理器短卡纸。 如果默认的处理器和 ITE 信息具有跟踪微型端口驱动程序，它可以将流量定向到其中已预期的上层。

请注意，虽然微型端口驱动程序必须跟踪对非活动状态的控制参数的所有更新，它们应延迟验证这些参数的 RSS 状态更改，使这些参数的尝试*active*。 例如，对于软件时禁用 RSS 的硬件进行传播，上层协议可用于任何处理器进行传播 （包括适配器的 RSS 集之外）。 上层，请确保，在 RSS 状态转换的时间点所有*处于非活动状态*参数都是有效的新的 RSS 状态。 但是，微型端口 dirver 应仍验证的参数，如果它发现的任何跟踪失败 RSS 状态转换*处于非活动状态*控制参数均无效。

### <a name="initial-state-and-updates-to-steering-parameters"></a>初始状态和控制参数的更新

下表介绍 （例如，VPort 在创建后），在创建后缩放的实体的初始状态以及可以如何更新参数：

| 参数 | 描述 |
| --- | --- |
| 主处理器 | <ul><li>初始化具有**相关性**VPort 创建过程中指定的处理器。</li><li>可以使用更新[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)与 OID **NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_PRIMARY_PROCESSOR**标志设置。</li><li>可以使用更新[OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md)与 OID **NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED**标志 （这是现有的 cmdlet 的兼容性路径的设置).</li><li>可以使用读取[OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md)与 OID **NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED** （这是现有的 cmdlet 的兼容性路径） 的标志。</li><li>默认处理器或间接寻址表的内容不会影响后初始化移动的主处理器。</li></ul> |
| 默认的处理器 | <ul><li>初始化具有**相关性**VPort 创建过程中指定的处理器。</li><li>可以使用更新[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)与 OID **NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_DEFAULT_PROCESSOR**标志设置。</li></ul> |
| 间接表 | <ul><li>**NumberOfIndirectionTableEntries**设置为**1**。</li><li>使用初始化的唯一项**相关性**VPort 创建过程中指定的处理器。</li><li>可以使用更新[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID。</li></ul> |

从对应的条目当前指向的处理器调用 Ite 和 （使用 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES） 的主/默认处理器的更新。 对于给定 VPort，较高层可确保没有 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid 移动 Ite 或一组在这些情况下，将发出主/默认处理器：

1. 虽然[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)正在进行中。
2. 启动后 VPort 删除序列。 例如，为上层发出集筛选器 OID 仅在完成移动 Ite 的最后一个 OID 后。

### <a name="rss-disablement"></a>RSS 停用

RSS 停用期间的上层协议可能会选择所有 Ite 都指向主处理器，然后发出 OID 禁用 RSS，或者它可能选择将间接寻址表作为-是和禁用 RSS。 在任一情况下，接收流量应以主处理器为目标。

RSSv2 维护允许上层协议以删除不使用第一个禁用 RSS VPort RSSv1 要求。 为上层可以接收筛选器设置上 VPort 为零，这样可确保不接收流量流经 VPort，然后继续进行 VPort 删除但不能禁用 RSS。 较高层可保证期间或之后 VPort 删除，将发出任何 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid。

在 RSS 停用和 VPort 删除，微型端口驱动程序需要采取措施的任何挂起的上一个队列移由于可能存在的内部操作。

### <a name="rssv2-invariants"></a>RSSv2 固定条件

上层协议可确保在执行管理功能之前不违反了重要的固定条件或 ITE 移动。 例如：

1. 减少的队列数之前, 的上限层可确保间接表不会不引用 VPort 比新的队列数更多的处理器。
2. 上层应该不会请求为 VPort 违反的队列的当前配置的数量的间接寻址表更新。 微型端口驱动程序应实施此规则，并返回一个故障。
3. 在更改之前的 VMMQ 限制适配器的间接寻址表条目数，较高层可确保间接表的内容被规范化为 2 的幂。

## <a name="related-links"></a>相关链接

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)

[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

[在 NDIS 6.80 同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)
