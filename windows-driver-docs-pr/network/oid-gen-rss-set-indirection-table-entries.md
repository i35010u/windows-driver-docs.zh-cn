---
title: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
description: 本主题介绍 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
ms.assetid: F59D861C-B7DB-4C28-8842-4FDBAE1B95F1
keywords: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES, OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b90bc6a0728d5b257fb1b5fe638d62ecb748b21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381349"
---
[!include[RSSv2 Beta Prerelease](../rssv2-beta-prerelease.md)]

# <a name="oidgenrsssetindirectiontableentries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES

向发送 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES OID [RSSv2](receive-side-scaling-version-2-rssv2-.md)-支持的微型端口驱动程序执行的单个间接移动表条目。 此 oid[同步 OID](synchronous-oid-request-interface-in-ndis-6-80.md)，这意味着它不能返回 NDIS_STATUS_PENDING。 将为它颁发作为仅方法请求，在 IRQL = = DISPATCH_LEVEL。 

此调用使用*XxxSynchronousOidRequest*入口点，其中*Xxx*可以是*微型端口*或*筛选器*具体取决于的类型收到请求后的驱动程序。 如果它看到 NDIS_STATUS_PENDING 返回状态，此入口点会导致检查系统错误。

使用 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://msdn.microsoft.com/library/windows/hardware/9AB69EC6-FE78-4242-89C7-D36AA16676BF)结构，以指示的微型端口适配器以同步方式执行的一组操作，其中每个操作移动单个条目的 RSS间接寻址到的目标指定 VPort 表指定的 CPU。

## <a name="remarks"></a>备注

此 OID 必须执行，并在颁发它的处理器上下文中完成。 微型端口驱动程序必须完全执行后返回到较高层的 NDIS_STATUS_SUCCESS 此 OID。 这意味着，微型端口驱动程序应准备好接收 NDIS_STATUS_SUCCESS 与第一次移动完成后立即在新的处理器上移动多个 Ite 的连续 OID 请求。 

> [!TIP]
> 完全执行此 OID 意味着微型端口驱动程序必须准备好成功尝试另一项操作来移动项。 它并不指定其中正在进行接收队列移动，这可以是源 CPU 或目标 CPU 后会指示流量。

上层协议发出 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 设置 Ite 和/或主数据库和默认处理器参数以指向不同的处理器。 

可以为颁发此 OID *active*或*处于非活动状态*流量控制的参数。 控制参数的详细信息，请参阅[接收方缩放版本 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)。 针对中的参数/Ite*处于非活动状态*状态下，应验证微型端口驱动程序，将其缓存直到下一个相关 RSS 状态更改 （启用或禁用） 的目标处理器。 此时，缓存会变得处理器编号*active* ，用于将流量定向。 更新到*active*参数 （这些也必须进行验证） 参数，应采取立即生效以将流量定向。

必须给微型端口适配器与颁发 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES *NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID*清除的标志。 这是因为数组中的不同元素所引用的不同 VPorts 的可能性。

此 OID 调用仅在 IRQL = DISPATCH_LEVEL =。

微型端口驱动程序应准备好处理至少任意数量的间接寻址表项移动动作为它们中播发[NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。 在中定义的这**NumberOfIndirectionTableEntriesPerNonDefaultVPort**或**NumberOfIndirectionTableEntriesForDefaultVPort**该结构的成员或**128**在本机 RSS 模式下。

微型端口驱动程序应尝试执行任意数量的条目，因为它们可以并更新**EntryStatus**的每个成员[NDIS_RSS_SET_INDIRECTION_ENTRY](https://msdn.microsoft.com/library/windows/hardware/4430E19F-C603-4C52-8FC8-C36197FD2996)与操作的结果。

### <a name="oid-handler-for-oidgenrsssetindirectiontableentries"></a>OID OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 的处理程序

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 的 OID 处理程序被预期行为，如下所示：

- 由于 OID 的同步调用类型，不允许的 NDIS_STATUS_PENDING 返回。
- 完成所有传入的项移动已发送到当前的 CPU （以前启动远程处理器上）。 
- 强烈建议的微型端口驱动程序执行参数验证通过。 如果不可行，请执行一个地验证和执行的数组项数。 具体而言，微型端口驱动程序应检查所有被引用的对象是否有效：
    - 返回在 NDIS_STATUS_PENDING **EntryStatus**字段不允许项。
    - 微型端口适配器存在并处于良好状态。 否则，设置**EntryStatus** NDIS_STATUS_ADAPTER_NOT_FOUND、 NDIS_STATUS_ADAPTER_NOT_READY 等项的字段。
    - 每个 VPort 存在并处于良好状态。 否则，设置**EntryStatus** NDIS_STATUS_INVALID_PORT、 NDIS_STATUS_INVALID_PORT_STATE 等项的字段。
    - 每个间接表条目索引是已配置的范围内。 此范围是任一 0xFFFF 或在 [0...NumberOfIndirectionTableEntries-1] 范围设置[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) OID。 0xFFFF 和 0xFFFE 条目索引具有特殊含义：0xFFFF 定义默认的处理器，而 0xFFFE 定义主处理器。 出现错误时，该处理程序设置**EntryStatus**到 NDIS_STATUS_INVALID_PARAMETER 条目的字段。
    - 较高层和微型端口驱动程序期望 ITE 指向当前处理器 （CPU 操作者） 在移动前。 换而言之，无法远程定向 ITE。 如果不为 true，则设置**EntryStatus**到 NDIS_STATUS_NOT_ACCEPTED 条目的字段。
    - 目标的所有处理器的有效期，并且是微型端口适配器的 RSS 集的一部分。 否则，设置**EntryStatus**到 NDIS_STATUS_INVALID_DATA 条目的字段。
- 随后或作为一部分参数验证通过，验证资源这种情况。 验证要完整批移动 （疏散） 后使用的队列数不超过**NumberOfQueues**集中[NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)结构在[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)请求。 否则，返回 NDIS_STATUS_NO_QUEUES。 NDIS_STATUS_NO_QUEUES 应该用于表示与配置的队列数的冲突的所有条件。 NDIS_STATUS_RESOURCES 仅应该用于指定暂时内存不足情况。
- 作为资源检查，为每个缩放实体 (例如，VPort) 的一部分微型端口驱动程序必须处理条件时点到 CPU 移开它当前的所有 Ite...

如果所有的上述检查通过，微型端口驱动程序应该可以无条件地应用新配置，并且必须设置**EntryStatus** NDIS_STATUS_SUCCESS 到每个条目的字段。

一般情况下，此 OID 的处理程序应非常轻量。 它不应调用 NDIS 或操作系统服务比其他可能的同步操作，例如自旋锁和[ **NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismconfigmsixtableentry)。

微型端口驱动程序不应调用 NDIS 来指出状态或即插即用事件。

微型端口驱动程序也不应使用接收/传输完成指示上下文中的 OID 此处理程序，因为这样做因此导致递归。 为上层可以调用接收上下文中的此 OID 或传输的指示。

### <a name="moving-all-indirection-table-entries"></a>移动所有间接表条目

微型端口驱动程序应识别和处理移动离开当前的 CPU 的所有间接表项的特殊请求。 由于 RSSv2 运行与单个项将移动，微型端口驱动程序必须保证整个操作的原子性。 微型端口驱动程序处理移动命令的相应数组时遇到批处理期间出现错误，应还原所有已执行的命令并将所有命令都标记为"失败"中每个命令**EntryStatus**字段。 上层协议始终需要包含标记为"succeeded"的所有命令或标记为"失败"的所有命令的"移动所有 Ite"批，并且它会假设流量服从生成的状态，（之前或之后都移动）。 如果为上层发现仅某些条目标记为"失败"，它将 bug 检查系统，然后指向微型端口驱动程序，因为原因。

若要帮助微型端口驱动程序的"移动所有 Ite"命令的处理和以避免死锁，上层协议中的对批中的组都移动命令**SwitchId + VPortId**字段，以便：

- 上层想要针对同一 VPort 一起，作为"移动所有"命令的一部分执行的命令位于总体的批处理中的连续。
- 微型端口驱动程序不应尝试执行整个批命令，可能会针对不同 VPorts，以"所有移动"的方式。 仅面向相同 VPort 的命令组 (具有相同标记**SwitchId + VPortId**对) 需要执行符合"所有移动"语义。
- 当为上层并不关心"移动所有"语义时，它可能会交错到相同 VPort 具有不同 VPort(s) 命令的命令。 在这种情况下，如果由于"的队列数"冲突，无法执行到同一个 VPort 命令的第二个组，微型端口驱动程序会标记该组中使用对应的状态代码 (NDIS_STATUS_NO_QUEUES) 并有责任在上层恢复。

例如，如果上层协议交错出现一的系列命令如下：

- `VPort=1 ITE[0,1]`
- `VPort=2 ITE[0]`
- `VPort=1 ITE[2]`

微型端口驱动程序不需要尝试以原子方式执行所有四个移动命令，或所有这三个移动命令`VPort=1`(`ITE[0,1,2]`)。 它只需要执行`VPort=1 ITE[0,1]`组中"所有移动"的方式，则`VPort=2 ITE[0]`组，然后`VPort=1 ITE[2]`。 所有这三个命令组可能具有不同的结果。 例如，对于组`VPort=1 ITE[0,1]`并`VPort=2 ITE[0]`可能会成功，和`VPort=1 ITE[2]`组可能会失败。 结果应反映在相应**EntryStatus**命令的每个结构的成员。 这样一来，微型端口驱动程序不需要采取的安全执行的总体批次 （例如，锁定整个适配器） 的预防措施。 仅这些命令目标特定 VPort 需要进行序列化，可以使用更精细地 VPort 每锁定，并且避免了某些死锁。

> [!NOTE]
> 命令项的整个组必须具有相同的项状态标记。

### <a name="error-conditions-and-status-codes"></a>错误情况和状态代码

发生错误时，此 OID 返回下面的状态代码：

| 状态代码 | 错误条件 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID 的格式不正确。 |
| NDIS_STATUS_INVALID_PARAMETER | 其他字段中，标头中或在自身的 OID （但不是在单个命令条目） 包含无效值。 |

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

- [接收方缩放版本 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://msdn.microsoft.com/library/windows/hardware/9AB69EC6-FE78-4242-89C7-D36AA16676BF)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://msdn.microsoft.com/library/windows/hardware/4430E19F-C603-4C52-8FC8-C36197FD2996)
- [NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)

