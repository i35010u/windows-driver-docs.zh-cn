---
title: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
description: 本主题介绍 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES
ms.assetid: F59D861C-B7DB-4C28-8842-4FDBAE1B95F1
keywords: OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES，OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES RSSv2
ms.date: 10/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b43ae8403d5201ccc60a043743d8bf14483d34
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210523"
---
[!include[RSSv2 Beta Prerelease](../includes/rssv2-beta-prerelease.md)]

# <a name="oid_gen_rss_set_indirection_table_entries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES OID 发送到支持[RSSv2](receive-side-scaling-version-2-rssv2-.md)的微型端口驱动程序，以执行单个间接表项的移动。 此 OID 为[同步 oid](synchronous-oid-request-interface-in-ndis-6-80.md)，这意味着它不能返回 NDIS_STATUS_PENDING。 它仅作为方法请求发出，在 IRQL = = DISPATCH_LEVEL。 

此调用使用*XxxSynchronousOidRequest*入口点，其中*Xxx*是*微型端口*或*筛选器*，具体取决于接收请求的驱动程序类型。 如果发现 NDIS_STATUS_PENDING 返回状态，则此入口点会导致系统 bug 检查。

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 使用[NDIS_RSS_SET_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entries)结构指示微型端口适配器以同步方式执行一组操作，其中每个操作都将指定 VPORT 的 RSS 间接寻址表的单个项移动到目标指定 CPU。

## <a name="remarks"></a>备注

此 OID 必须在发出它的处理器上下文中执行和完成。 微端口驱动程序必须在将 NDIS_STATUS_SUCCESS 返回到上层时完全执行此 OID。 这意味着微型端口驱动程序应准备好接收返回的 OID 请求，以便在第一次移动 NDIS_STATUS_SUCCESS 完成后立即接收到新处理器上的多个 ITEs。 

> [!TIP]
> 完全执行此 OID 意味着微型端口驱动程序必须准备好，才能成功尝试另一个操作来移动 I)。 它并不规定在队列移动后（可以在源 CPU 或目标 CPU 上）直接指定正在进行的接收流量的位置。

上层协议问题 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 将 ITEs 和/或主和默认处理器参数设置为指向不同的处理器。 

可以为*活动*或*非活动*流量控制参数发出此 OID。 有关方向盘参数的详细信息，请参阅[接收方缩放版本2（RSSv2）](receive-side-scaling-version-2-rssv2-.md)。 对于处于*非活动*状态的参数/ITEs，微型端口驱动程序应该验证并缓存目标处理器，直到下一个相关 RSS 状态更改（启用或禁用）。 此时，缓存的处理器编号将变为*活动状态*，并用于定向流量。 应立即将对*活动*参数的更新（还必须验证）进行更新，以指示流量。

必须将 OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 颁发给已清除*NDIS_OID_REQUEST_FLAGS_VPORT_ID_VALID*标志的微型端口适配器。 这是因为数组中的不同元素可能会引用不同的 VPorts。

此 OID 仅在 IRQL = = DISPATCH_LEVEL 调用。

小型端口驱动程序应准备好处理在[NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构中播发时所需的最少数量的间接寻址表项移动操作。 这是在该结构的**NumberOfIndirectionTableEntriesPerNonDefaultVPort**或**NumberOfIndirectionTableEntriesForDefaultVPort**成员中定义的，或者是在本机 RSS 模式下的**128**中定义的。

微型端口驱动程序应尝试执行尽可能多的条目，并将每个[NDIS_RSS_SET_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entry)的**EntryStatus**成员更新为操作结果。

### <a name="oid-handler-for-oid_gen_rss_set_indirection_table_entries"></a>OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 的 OID 处理程序

OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES 的 OID 处理程序的行为应如下所示：

- 由于 OID 的同步调用类型，不允许返回 NDIS_STATUS_PENDING。
- 完成目标为当前 CPU （以前在远程处理器上启动）的任何传入 I) 移动。 
- 强烈建议使用微型端口驱动程序来执行完整参数验证。 如果不可能，请逐个执行验证和执行数组项。 微型端口驱动程序应专门检查所有被引用对象是否有效：
    - 不允许在 I) 的**EntryStatus**字段中返回 NDIS_STATUS_PENDING。
    - 微型端口适配器存在并且处于良好状态。 否则，将条目的 " **EntryStatus** " 字段设置为 NDIS_STATUS_ADAPTER_NOT_FOUND、NDIS_STATUS_ADAPTER_NOT_READY 等。
    - 每个 VPort 都存在并且处于良好状态。 否则，将条目的 " **EntryStatus** " 字段设置为 NDIS_STATUS_INVALID_PORT、NDIS_STATUS_INVALID_PORT_STATE 等。
    - 每个间接表项索引在配置的范围内。 此范围为0xFFFF 或处于由[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md) OID 设置的 [0 ... NumberOfIndirectionTableEntries-1] 范围内。 0xFFFF 和0xFFFE 条目索引具有特殊含义：0xFFFF 定义默认的处理器，而0xFFFE 定义主处理器。 出现错误时，处理程序将该项的**EntryStatus**字段设置为 NDIS_STATUS_INVALID_PARAMETER。
    - 上层和微型端口驱动程序预计在移动之前，I) 指向当前处理器（执行组件 CPU）。 换句话说，I) 不能远程重定向。 如果不是这种情况，请将条目的 " **EntryStatus** " 字段设置为 NDIS_STATUS_NOT_ACCEPTED。
    - 所有目标处理器都是有效的，并且是小型端口适配器的 RSS 集的一部分。 否则，将条目的 " **EntryStatus** " 字段设置为 "NDIS_STATUS_INVALID_DATA"。
- 或者作为参数验证传递的一部分，验证资源的情况。 验证在[OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)请求期间，在完整批处理移动（疏散）后要使用的队列数是否未超过[NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)结构中设置的**NumberOfQueues** 。 否则，将返回 NDIS_STATUS_NO_QUEUES。 NDIS_STATUS_NO_QUEUES 应用于表示与配置的队列数冲突的所有条件。 NDIS_STATUS_RESOURCES 应仅用于指定暂时性内存不足的情况。
- 在资源检查过程中，对于每个缩放实体（例如，VPort），微型端口驱动程序必须在指向 currrent CPU 的所有 ITEs 移出时处理条件。

如果上述所有检查都通过，微型端口驱动程序应能够无条件地应用新配置，并且必须将每个条目的**EntryStatus**字段设置为 NDIS_STATUS_SUCCESS。

通常，此 OID 的处理程序应该非常轻量。 对于可能的同步操作（如旋转锁和[**NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismconfigmsixtableentry)），它不应调用 NDIS 或操作系统服务。

微型端口驱动程序不应调用 NDIS 来指示状态或 PnP 事件。

小型端口驱动程序也不应在此 OID 处理程序的上下文中使用接收/传输完成指示，因为这样会导致递归。 上层可以从接收或发送指示的上下文中调用此 OID。

### <a name="moving-all-indirection-table-entries"></a>移动所有的间接寻址表项

微型端口驱动程序应识别并处理一个特殊的请求，该请求将所有间接表条目移出当前 CPU。 由于 RSSv2 操作的是单个 I) 移动，因此微型端口驱动程序必须保证总体操作的原子性。 如果在处理相应的移动命令数组时在批处理中间遇到错误，微型端口驱动程序应还原所有已执行的命令，并在每个命令**EntryStatus**字段中将所有命令标记为 "失败"。 上层协议始终需要 "移动所有 ITEs" 批处理才能包含标记为 "succeeded" 的所有命令或标记为 "失败" 的所有命令，并且它将假定流量服从产生状态（移动之前或之后）。 如果上层仅看到某些标记为 "失败" 的项，它将错误检查系统，并将其指向微型端口驱动程序作为原因。

为了帮助微型端口驱动程序对 "移动所有 ITEs" 命令的处理，并避免死锁，上层协议组**SwitchId + VPortId**字段对批处理中的移动命令，以便：

- 上层要一起执行的命令，作为相同 VPort 的 "全部移动" 命令的一部分，在整个批处理中连续放置。
- 微型端口驱动程序不应尝试执行整个命令批处理，该批处理以 "全部移动" 的方式面向不同的 VPorts。 只需执行针对相同 VPort 的命令组（标记为同一**SwitchId + VPortId**对），才能符合 "移动全部" 语义。
- 如果上层并不关心 "全部移动" 语义，则它可能会将命令与不同 VPort 的命令进行 VPort。 在这种情况下，如果由于存在 "队列数量" 冲突而导致第二组命令无法执行，则微型端口驱动程序会使用相应的状态代码（NDIS_STATUS_NO_QUEUES）来标记该组，并使用上层来负责从中.

例如，如果上层协议交错一系列命令，如下所示：

- `VPort=1 ITE[0,1]`
- `VPort=2 ITE[0]`
- `VPort=1 ITE[2]`

微型端口驱动程序无需尝试以原子方式执行所有四个移动命令，或所有三个移动命令用于 `VPort=1` （`ITE[0,1,2]`）。 它只需以 "移动全部" 的方式执行 `VPort=1 ITE[0,1]` 组，然后以 `VPort=2 ITE[0]` 组的形式执行，然后 `VPort=1 ITE[2]`。 这三个命令组可能会有不同的结果。 例如，`VPort=1 ITE[0,1]` 和 `VPort=2 ITE[0]` 的组可能会成功，并且 `VPort=1 ITE[2]` 组可能会失败。 结果应在每个命令结构的相应**EntryStatus**成员中反映出来。 这样一来，微型端口驱动程序无需采取措施来安全地执行整个批处理（例如锁定整个适配器）。 只有面向特定 VPort 的命令需要进行序列化，可使用更细粒度的 VPort 锁定，并避免某些死锁。

> [!NOTE]
> 整个命令条目组必须标记为相同的条目状态。

### <a name="error-conditions-and-status-codes"></a>错误情况和状态代码

当发生错误时，此 OID 返回以下状态代码：

| 状态代码 | 错误条件 |
| --- | --- |
| NDIS_STATUS_INVALID_LENGTH | OID 的格式不正确。 |
| NDIS_STATUS_INVALID_PARAMETER | 其他字段（在标头中或 OID 本身中，而不是在单独的命令项中）包含无效的值。 |

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

- [接收方缩放版本2（RSSv2）](receive-side-scaling-version-2-rssv2-.md)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entries)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entry)
- [NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)

