---
title: 接收端缩放版本 2 (RSSv2)
description: '本主题描述接收方缩放版本 2 (RSSv2) '
keywords: 接收方缩放版本2，RSSv2，接收方缩放版本 2 WDK，RSSv2 网络驱动程序
ms.date: 10/12/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e51f462c961eacf03adeaba731e419917f9a282
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829179"
---
# <a name="receive-side-scaling-version-2-rssv2"></a>接收端缩放版本 2 (RSSv2)

接收方缩放改善了与处理多处理器系统上的网络数据相关的系统性能。 NDIS 6.80 和更高版本支持 RSS 版本 2 (RSSv2) ，它通过提供动态的 VPort 分散队列来扩展 RSS。

## <a name="overview"></a>概述

与 RSSv1 相比，RSSv2 缩短了 CPU 负载度量值与间接表更新之间的时间。 这可以避免在高流量情况下出现缓慢。 若要完成此操作，RSSv2 将在处理请求的处理器上下文中以 IRQL = DISPATCH_LEVEL 执行其操作，并且仅对指向当前处理器的间接表条目的子集执行操作。 这意味着，RSSv2 可通过多个处理器动态分散接收队列，对象比 RSSv1 多。

RSSv2 中引入了两个 Oid （ [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) 和 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)），它们可用于设置正确的 RSS 功能并分别控制间接寻址表。 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 是常规 OID，而 OID_GEN_RSS_SET_INDIRECTION_ENTRIES 是无法返回 NDIS_STATUS_PENDING 的同步 OID。 有关这些 Oid 的详细信息，请参阅各自的参考页。 有关同步 Oid 的详细信息，请参阅 [NDIS 6.80 中的同步 oid 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)。

## <a name="rssv2-terminology"></a>RSSv2 术语

本主题使用以下术语：

| 术语 | 定义 |
| --- | --- |
| RSSv1 | 第一代接收方缩放机制。 使用 [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)。 |
| RSSv2 | 本主题中所述的 Windows 10 版本1803及更高版本中支持第二代接收方缩放机制。 |
| 缩放实体| 本机 RSS 模式下的微型端口适配器本身，或处于 RSSv2 模式下的 VPort。 |
| I） | 间接表条目 (给定缩放实体的 I) ) 。 每个 VPort 的 ITEs 总数不能超过 VMQ 模式下的 **NumberOfIndirectionTableEntriesPerNonDefaultPFVPort** 或 **NumberOfIndirectionTableEntriesForDefaultVPort** ，也不能在本机 RSS 案例中128。 **NumberOfIndirectionTableEntriesPerNonDefaultPFVPort** 和 **NumberOfIndirectionTableEntriesForDefaultVPort** 是 [NDIS_NIC_SWITCH_CAPABILITIES](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities) 结构的成员。 |
| 缩放模式 | VPort vmswitch 策略，用于控制在运行时如何处理其 ITEs。 这可以是静态的 (由于负载更改) 或动态 (扩展和合并（具体取决于当前流量负载) ）。 |
| 队列 | 支持 I) 的底层硬件对象 (队列) 。 根据硬件和间接寻址表，配置队列可能会返回多个 ITEs。 队列的总数，包括默认队列使用的队列总数，不能超过通常由管理员设置的预配置限制。 |
| 默认处理器 | 接收无法为其计算哈希的数据包的处理器。 每个 VPort 都有一个默认处理器。
| 主处理器 | 在 VPort 创建期间指定为 [NDIS_NIC_SWITCH_VPORT_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的 **ProcessorAffinity** 成员的处理器。 此处理器可在运行时进行更新，并指定要定向到 VMQ 流量的位置。 |
| 源 CPU | I) 当前映射到的处理器。 |
| 目标 CPU | 要 (使用 RSSv2) 将 I) 重新映射到的处理器。 |
| 执行组件 CPU | 发出 RSSv2 请求的处理器。 |

## <a name="advertising-rssv2-capability-in-a-miniport-driver"></a>在微型端口驱动程序中公布 RSSv2 功能

微型端口驱动程序通过使用 *NDIS_RSS_CAPS_SUPPORTS_INDEPENDENT_ENTRY_MOVE* 标志设置 [NDIS_RECEIVE_SCALE_CAPABILITIES](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)结构的 **CapabilitiesFlags** 成员播发 RSSv2 支持。 启用 RSSv2's CPU 负载平衡功能需要此功能，同时提供 *NDIS_RECEIVE_FILTER_DYNAMIC_PROCESSOR_AFFINITY_CHANGE_SUPPORTED* 标志，为非默认 VPorts (vmq) 启用 RSSv1 动态平衡。

> [!NOTE]
> 上层协议假设可为 RSSv2 微型端口驱动程序移动默认 VPort 的主处理器。

如果微型端口适配器未播发 RSSv2 功能，则即使这些 VPorts 请求执行动态传播，所有启用 VMQ 的 VPorts 仍保持静态分配模式。 用于配置 RSS 参数 [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md)的 RSSv1 OID 用于仍处于静态扩散模式下的这些 VPorts。

微型端口驱动程序只需实现一种 RSS 控制机制，即 RSSv1 或 RSSv2。 如果驱动程序公布 RSSv2 支持，则在需要时，NDIS 会将 RSSv1 Oid 转换为 RSSv2 Oid，以 congifure 每个 VPort 的传播。 微型端口驱动程序必须支持两个新的 Oid，并按如下所示修改 RSSv1 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 的行为：

- [OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md) 仅用于 RSSv2 中的查询请求，而不用于设置 RSS 参数。
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) 是一种用于配置缩放实体的参数（例如队列数、ITEs 数、RSS 启用/禁用和哈希密钥更新）的查询和集 OID。
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) 是用于对间接表项进行修改的方法 OID。

## <a name="handling-rssv2-oids"></a>处理 RSSv2 Oid

[OID_GEN_RECEIVE_SCALE_PARAMETERS](oid-gen-receive-scale-parameters.md) 仅用于查询给定缩放实体的当前 RSS 参数。 在 RSSv1 中，此 OID 用于设置参数。 对于支持 RSSv2 的微型端口驱动程序，NDIS 会自动为驱动程序执行此角色转换，并发出以下两个 Oid 来改为设置参数。

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) 是一个常规 oid，并与在 RSSv1 中处理 OID_GEN_RECEIVE_SCALE_PARAMETERS OID 的处理方式相同。 此 OID 对于 ndis 6.80 之前 (LWFs) 的 NDIS 轻型筛选器驱动程序不可见。

但[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)是无法返回 NDIS_STATUS_PENDING 的[同步 OID](synchronous-oid-request-interface-in-ndis-6-80.md) 。 必须在生成 OID 的处理器上下文中执行并完成此 OID。 与 OID_GEN_RECEIVE_SCALE_PARAMETERS_V2 一样，在 NDIS 6.80 之前，它也不会对 NDIS LWFs 可见。 不允许在 NDIS 6.80 和更高版本中使用 LWFs 将此 OID 延迟或移动到另一个处理器。 其负载包含简单的 "move I) " 操作的数组，其中每个操作都包含一个命令，用于将缩放实体的单个 I) 移动到不同的目标 CPU。 数组元素可以引用不同的缩放实体 (VPorts) 。

每种类型的 NDIS 驱动程序、微型端口、筛选器和协议都具有支持同步 OID 请求接口的入口点：

| NDIS 驱动程序类型 | 同步 OID 处理程序 (s)  | 用于发起同步 Oid 的函数 |
| --- | --- | --- |
| 小型 | [*MiniportSynchronousOidRequest*](/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request) | 空值 |
| 筛选器 | <ul><li>[*FilterSynchronousOidRequest*](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request)</li><li>[*FilterSynchronousOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request_complete)</li></ul> | [**NdisFSynchronousOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsynchronousoidrequest) |
| 协议 | 空值 | [**NdisSynchronousOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest) |

## <a name="rss-state-transitions-ite-updates-and-primarydefault-processors"></a>RSS 状态转换、I) 更新和主/默认处理器

### <a name="steering-parameters"></a>方向盘参数

在 RSSv2 中，使用不同的参数将流量引导到正确的 CPU，具体取决于启用或禁用)  (启用或禁用的 RSS 状态。 禁用 RSS 后，只会使用主处理器来定向流量。 启用 RSS 后，默认处理器和所有 ITEs 都将用于定向流量。 这些控制 *参数* labele 为 "活动" 或 "非活动"，下表对此进行了总结：

| 方向盘参数 | 已禁用 RSS | 已启用 RSS |
| --- | --- | --- |
| 主处理器 | 可用 | 非活动 |
| 默认处理器 | 非活动 | 可用 |
| I) [0 ... N] | 非活动 | 可用 |

当某个控制参数处于 *活动* 状态时，它会定向该流量。 从使参数 *处于非活动* 状态的 RSS 状态转换的那一刻起，微型端口驱动程序必须跟踪对参数所做的更改，直到反向转换再次激活它。 这意味着，在为该缩放实体禁用 RSS 时，微型端口驱动程序需要跟踪对默认处理器和间接表条目的所有更新。 启用 RSS 后，默认处理器和间接寻址表的当前跟踪状态应生效。

例如，假设已启用软件 vRSS。 在这种情况下，此间接寻址表已经存在于上层协议中，并且由上层的软件传播代码主动使用。 如果在硬件 RSS 启用过程中，所有项在 *移动* 间接表项的更新被颁发给并由硬件执行之前，开始指向主处理器，则主处理器可能会出现短暂的堵塞。 如果微型端口驱动程序跟踪了默认的处理器和 I) 信息，则它可以将流量定向到上层的预期位置。

请注意，微型端口驱动程序必须跟踪对非活动控制参数的所有更新，而它们应延迟对这些参数的验证，直到 RSS 状态更改尝试使这些参数变为 *活动* 状态。 例如，在软件传播的情况下，如果禁用了硬件 RSS，则上层协议可以使用任何处理器进行传播， (包括适配器的 RSS 集) 之外。 上层确保在 RSS 状态转换时，所有 *非活动* 参数对于新的 RSS 状态都有效。 但是，如果发现任何跟踪的 *非活动* 控制控制参数无效，微型端口 dirver 仍应验证参数，并使 RSS 状态转换失败。

### <a name="initial-state-and-updates-to-steering-parameters"></a>对方向盘参数的初始状态和更新

下表描述了创建之后 (缩放实体的初始状态，例如，在创建 VPort 后) ，以及如何更新参数：

| 参数 | 描述 |
| --- | --- |
| 主处理器 | <ul><li>用 VPort 创建期间指定的 **关联** 处理器进行了初始化。</li><li>可以使用 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID，并设置 **NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_PRIMARY_PROCESSOR** 标志。</li><li>可以使用 [OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md) OID 进行更新，并设置 **NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED** 标志， (这是现有 cmdlet 的) 的兼容路径。</li><li>可使用带有 **NDIS_NIC_SWITCH_VPORT_PARAMS_PROCESSOR_AFFINITY_CHANGED** 标志的 [OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md) OID 读取， (这是现有 cmdlet 的) 的兼容路径。</li><li>主处理器的初始化后移动不会影响默认处理器或间接表的内容。</li></ul> |
| 默认处理器 | <ul><li>用 VPort 创建期间指定的 **关联** 处理器进行了初始化。</li><li>可以使用 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID，并设置 **NDIS_RSS_SET_INDIRECTION_ENTRY_FLAG_DEFAULT_PROCESSOR** 标志。</li></ul> |
| 间接寻址表 | <ul><li>**NumberOfIndirectionTableEntries** 设置为 **1**。</li><li>只有在创建 VPort 的过程中指定的 **关联** 处理器才会初始化该条目。</li><li>可以使用 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID 进行更新。</li></ul> |

使用 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES) 进行的 ITEs 更新和主/默认处理器 (从相应条目当前指向的处理器调用。 对于给定的 VPort，上层确保在这些情况下不会发出用于移动 ITEs 或设置主/默认处理器的 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid：

1. [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)正在进行。
2. 启动 VPort 删除序列之后。 例如，上层仅在完成最后一个要移动 ITEs 的 OID 后发出集筛选器 OID。

### <a name="rss-disablement"></a>RSS 禁用

在 RSS 禁用期间，上层协议可能会选择将所有 ITEs 指向主处理器，然后发出 OID 来禁用 RSS，或者可能选择将间接表保持原样并禁用 RSS。 在任一情况下，接收流量应以主处理器为目标。

RSSv2 维持了 RSSv1 的要求，该要求允许上层协议删除 VPort，而无需首先禁用 RSS。 上层可以将 VPort 上的接收筛选器设置为零，从而确保没有任何接收流量流过 VPort，然后继续进行 VPort 删除而不禁用 RSS。 上层保证在 VPort 删除期间或之后不会发出任何 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES Oid。

在 RSS 禁用和 VPort 的删除过程中，微型端口驱动程序应负责处理由于上一队列移动而可能存在的任何挂起的内部操作。

### <a name="rssv2-invariants"></a>RSSv2 固定条件

上层协议可确保在执行管理功能或 I) 移动之前不违反重要的固定条件。 例如：

1. 在减少队列数量之前，上层可确保间接寻址表不会引用超过 VPort 的新队列数的处理器。
2. 上层不应请求与当前配置的 VPort 数冲突的间接表更新。 微型端口驱动程序应强制执行此错误，并返回一个失败。
3. 在更改 VMMQ 限制的适配器的间接寻址表条目数之前，上层将确保间接寻址表的内容标准化为2的幂。

## <a name="related-links"></a>相关链接

[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)

[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)

[NDIS 6.80 中的同步 OID 请求接口](synchronous-oid-request-interface-in-ndis-6-80.md)
