---
title: OID_SWITCH_NIC_REQUEST
description: 对象标识符 (OID) 方法请求 OID_SWITCH_NIC_REQUEST 用于封装和转发到 Hyper-v 可扩展交换机外部网络适配器的 OID 请求。
ms.assetid: 7EF4D950-D18E-400A-B1DD-39768A16E4C4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_REQUEST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f0b7f7f9c86f19b28c8b24141273a9935df817e6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212151"
---
# <a name="oid_switch_nic_request"></a>OID \_ 交换机 \_ NIC \_ 请求


 (oid 的对象标识符) 方法请求 OID \_ 交换机 \_ NIC \_ 请求用于将 oid 请求封装并转发到 hyper-v 可扩展交换机外部网络适配器。 这允许将封装的 OID 请求传递到绑定到外部网络适配器的底层物理网络适配器的驱动程序。

此 OID 请求还用于封装向连接到可扩展交换机端口的其他网络适配器发出的 OID 请求。 在这种情况下，封装的 OID 请求将通过可扩展交换机驱动程序堆栈转发，以便通过扩展进行检查。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构的指针。 此结构指定 OID 请求的转发信息。 此结构还包含一个指针，指向要转发的 OID 请求的原始 **NDIS \_ OID \_ 请求** 结构。

<a name="remarks"></a>备注
-------

当 OID 请求到达 Hyper-v 可扩展交换机接口时，它将对其进行封装，以便将它们向下扩展到可扩展的交换机控制路径。 这些 OID 请求包括：

-   硬件卸载 OID 请求，包括对 Internet 协议安全 (IPsec) 、虚拟机队列 (VMQ) 和单一根 i/o 虚拟化 (SR-IOV) 的请求。 这些 OID 请求由在 Hyper-v 父分区的管理操作系统中运行的过量协议或筛选器驱动程序发出。

    当这些 OID 请求到达可扩展交换机接口时，可扩展交换机的协议边缘将在 [**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request) 结构内封装 OID 请求。 协议边缘按以下方式设置此结构的成员：

    -   **DestinationPortId**和**DestinationNicIndex**成员设置为外部网络适配器的相应值。

    -   如果 OID 请求源自 Hyper-v 子分区，则 **SourcePortId** 和 **SourceNicIndex** 成员将设置为分区所使用的端口和网络适配器的相应值。 否则， **SourcePortId** 和 **SourceNicIndex** 成员将设置为零。

        **注意**  如果扩展或重定向 OID 请求，扩展必须保留这些成员的值。



    -   **OidRequest**成员设置为指向封装的 oid 请求的[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的指针。

    然后，协议边缘发出 OID \_ 交换机 \_ NIC \_ 请求请求，以将封装的 OID 请求向下转发到外部网络适配器的可扩展交换机控制路径。

    基础转发扩展可将封装的硬件卸载 OID 请求重定向到绑定到外部网络适配器的物理网络适配器。 例如，如果扩展插件支持绑定到外部网络适配器的可扩展交换机组中的物理网络适配器，则可以将 OID \_ 交换机 \_ NIC \_ 请求请求转发到负载平衡故障转移 (LBFO) 组中支持硬件卸载的物理适配器。 有关此过程的详细信息，请参阅 [管理对物理网络适配器的硬件卸载 OID 请求](./managing-hardware-offload-oid-requests-to-physical-network-adapters.md)。

    有关可扩展交换机团队的详细信息，请参阅 [物理网络适配器配置的类型](./types-of-physical-network-adapter-configurations.md)。

-   多播 OID 请求，包括 [OID \_ 802 \_ 3 \_ 添加 \_ 多播 \_ 地址](oid-802-3-add-multicast-address.md) 和 [oid \_ 802 \_ 3 \_ 删除 \_ 多播 \_ 地址](oid-802-3-delete-multicast-address.md)。 这些 OID 请求由过量协议和筛选器驱动程序（在 Hyper-v 子分区的管理操作系统或来宾操作系统中运行）发出。

    当这些 OID 请求到达可扩展交换机接口时，可扩展交换机的协议边缘将在 [**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request) 结构内封装 OID 请求。 协议边缘还会将 **SourcePortId** 和 **SourceNicIndex** 成员设置为从中发出 OID 请求的端口和网络适配器的相应值。 然后，协议边缘发出 OID \_ 交换机 \_ NIC \_ 请求请求，以将封装的 OID 请求向下转发到由基础扩展进行检查的可扩展交换机控制路径。

    **注意**  在这种情况下，协议边缘会将 **DestinationPortId** 和 **DestinationNicIndex** 成员设置为零。 这指定封装的 OID 请求将传递到控件路径中的扩展。

    基础转发扩展可以检查这些封装的 OID 请求并保留它们指定的多播地址信息。 例如，如果扩展会将多播数据包转发到可扩展交换机端口，则可能需要此信息。

    有关详细信息，请参阅 [从 Hyper-v 子分区转发 OID 请求](./forwarding-oid-requests-from-a-hyper-v-child-partition.md)。

转发扩展还可以发出 OID \_ 交换机 \_ NIC 请求，以便 \_ 将封装的 OID 请求转发到绑定到外部网络适配器的物理网络适配器。 这允许扩展产生自己的 OID 请求，或将现有的 OID 请求重定向到绑定到外部网络适配器的物理网络适配器。 为了执行此操作，扩展必须执行以下步骤：

1.  扩展调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 来递增目标物理网络适配器的索引的引用计数器。 这可确保在其引用计数器为非零的情况下，可扩展交换机接口将不会删除物理网络适配器连接。

    **注意**  如果物理网络适配器的引用计数器为非零，则可扩展交换机接口可能会断开与该连接的连接。 有关详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

2.  此扩展通过按以下方式初始化 [**NDIS \_ 交换机 \_ NIC \_ oid \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request) 结构来封装 OID 请求：

    -   **DestinationPortId**成员必须设置为外部网络适配器连接到的可扩展交换机端口的标识符。
    -   **DestinationNicIndex**成员必须设置为底层物理网络适配器的非零索引值。
    -   如果扩展是代表 Hyper-v 子分区建立的，则 **SourcePortId** 和 **SourceNicIndex** 成员将设置为分区所使用的端口和网络适配器的相应值。 否则， **SourcePortId** 和 **SourceNicIndex** 成员将设置为零。

        例如，如果扩展插件管理的是子分区的硬件卸载资源，则必须设置 **SourcePortId** 和 **SourceNicIndex** 成员，以指定封装的硬件卸载 OID 请求适用的分区。

    -   必须将 **OidRequest** 成员设置为指向封装的 oid 请求的已初始化 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构的指针。

3.  该扩展调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将 OID 请求转发到指定的目标可扩展交换机端口和网络适配器。

4.  当 NDIS 调用 [*FilterOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) 函数时，扩展会调用 [*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) ，以清除目标物理网络适配器的索引的引用计数器。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 交换机 NIC 请求的 OID 查询 \_ 请求 \_ \_ ，并返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，请求失败。</p></td>
</tr>
</tbody>
</table>



<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)