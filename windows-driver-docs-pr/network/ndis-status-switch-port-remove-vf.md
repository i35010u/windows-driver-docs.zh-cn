---
title: NDIS_STATUS_SWITCH_PORT_REMOVE_VF
description: NDIS_STATUS_SWITCH_PORT_REMOVE_VF 状态指示由 Hyper-v 可扩展交换机转发扩展颁发，用于删除虚拟机（VM）网络适配器与 PCI Express （PCIe）虚拟功能（VF）之间的绑定。
ms.assetid: D6A52183-C9C6-4F0B-9E25-6C5C16CBEFFE
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_SWITCH_PORT_REMOVE_VF 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 548e390ce33177a7cf21484c973bf1d24be194a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843511"
---
# <a name="ndis_status_switch_port_remove_vf"></a>NDIS\_状态\_交换机\_端口\_删除\_VF


**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示由 hyper-v 可扩展交换机转发扩展颁发，以删除虚拟机（VM）网络适配器与 PCI 之间的绑定Express （PCIe）虚函数（VF）。 VF 由支持单根 i/o 虚拟化（SR-IOV）接口的底层物理网络适配器公开和支持。

为了 **\_状态\_交换机\_端口发出 NDIS，\_删除\_VF**状态指示，转发扩展必须在[ **\_NIC\_状态的 NDIS\_交换机中封装指示\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构并[ **\_交换机\_NIC\_状态状态指示发出 NDIS\_状态**](ndis-status-switch-nic-status.md)。

有关此过程的详细信息，请参阅[ **\_交换机\_端口发出 NDIS\_状态的准则\_删除\_VF**状态指示](#issuing)。

<a name="remarks"></a>备注
-------

PCIe VF 由支持 SR-IOV 接口的基础物理适配器创建和分配。 创建后，虚拟化堆栈会将 VF 附加或*分配*到 hyper-v 子分区。 在此分区中运行的来宾操作系统将公开一个虚拟机（VM）网络适配器，该适配器绑定到基础 SR-IOV 物理适配器的 VF。

分配虚拟和物理网络适配器后，会直接在 VF 与 VM 网络适配器之间路由数据包。 但是，因为可扩展交换机不涉及数据包传递，所以可扩展交换机端口策略不会应用于这些数据包。 这包括访问控制列表（Acl）和服务质量（QoS）的端口策略。

可扩展的交换机转发扩展可以通过发出**NDIS\_状态\_交换机\_端口**来删除将 vf 分配给子分区，\_删除\_VF 状态指示。 此指示会导致数据包通过可扩展交换机端口发送，而不是直接在 VM 网络适配器和基础 SR-IOV 物理适配器的 VF 之间传输。 这允许将可扩展交换机端口策略应用到通过可扩展交换机端口接收或发送的数据包。

当转发扩展使**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示，它将指定 VM 网络适配器连接到的可扩展交换机端口。

有关可扩展交换机转发扩展的详细信息，请参阅[转发扩展](https://docs.microsoft.com/windows-hardware/drivers/network/forwarding-extensions)。

### <a href="" id="issuing"></a>\_交换机\_端口发出 NDIS\_状态的准则\_删除\_VF 状态指示

为了 **\_状态\_交换机\_端口发出 NDIS，\_删除\_VF**状态指示，转发扩展必须执行以下步骤：

1.  转发扩展插件为**ndis\_\_状态**初始化[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构，\_\_\_删除 VF 指示。 对于这一指示，转发扩展会将**NDIS\_状态**的以下成员设置\_指示结构：

    -   必须将**StatusCode**成员设置为**NDIS\_状态\_交换机\_端口\_删除\_VF**。

    -   **StatusBuffer**成员必须设置为**NULL**。

    -   **StatusBufferSize**必须设置为零。

2.  转发扩展插件[ **\_NIC\_状态\_指示结构初始化 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)。 为了删除 VF 分配，转发扩展必须按以下方式设置成员：

    -   **DestinationPortId**成员必须设置为 VM 网络适配器连接到的可扩展交换机端口的标识符。

    -   **DestinationNicIndex**成员必须设置为连接到指定端口的 VM 网络适配器的索引值。

    -   必须将**SourcePortId**成员设置为**NDIS\_交换机\_默认\_端口\_ID**。

    -   必须将**SourceNicIndex**成员设置为**NDIS\_交换机\_默认\_NIC\_索引**。

    -   必须将**StatusIndication**成员设置为 NDIS\_状态的[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的地址 **\_SWITCH\_端口\_删除\_VF**指示。

3.  转发扩展插件会\_将 ndis 的[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构初始化为[ **\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)指示。 对于此指示，转发扩展会将**NDIS\_状态**的以下成员设置\_指示结构：

    -   必须将**StatusCode**成员设置为[**NDIS\_状态\_交换机\_NIC\_状态**](ndis-status-switch-nic-status.md)。

    -   必须将**StatusBuffer**成员设置为[**NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的地址。

    -   必须将**StatusBufferSize**设置为 NDIS\_交换机的长度（以字节为单位） [ **\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构， [**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构 **\_状态\_切换\_端口\_删除\_VF**指示。

4.  转发扩展必须调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)来递增 VM 网络适配器的引用计数器。 如果*ReferenceSwitchNic*未完成，NDIS\_状态\_成功，则转发扩展不能转发状态指示。

    **请注意**  转发扩展是否已收到[OID\_交换机\_NIC\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)VM 适配器的断开设置请求，它不得调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，也不能转发状态指示。

     

5.  转发扩展插件调用[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) ，将[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)转发到可扩展交换机驱动程序堆栈中的过量扩展。 当转发扩展插件调用此函数时，它会将*StatusIndication*参数设置为指向 ndis 的指针的指针 **\_状态\_指示**结构的[**ndis\_状态\_交换机\_NIC\_状态**](ndis-status-switch-nic-status.md)指示。

6.  [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)返回后，转发扩展必须调用[*DEREFERENCESWITCHNIC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)来减小 VM 网络适配器的引用计数器。

**请注意**  转发扩展必须遵循转发扩展要删除的每个 VF 分配的前面的步骤。

 

有关转发扩展转发状态指示的详细信息，请参阅[筛选模块状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/filter-module-status-indications)。

### <a name="guidelines-for-determining-vf-assignments"></a>确定 VF 分配的准则

转发扩展插件可以通过发出 oid [\_SWITCH\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)的 oid 查询请求来枚举虚拟网络适配器的当前 VF 分配。 此请求返回[**ndis\_交换机\_nic\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)结构，该结构包含一组[**ndis\_switch\_nic\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构。 每个**NDIS\_交换机\_NIC\_参数**结构指定在以下环境之一中公开的网络适配器的参数：

-   在 Hyper-v 父分区中运行的管理操作系统。

    在此操作系统中公开的网络适配器使用[**NDIS\_交换机\_NIC\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)枚举值指定为**NdisSwitchNicTypeExternal**或**NdisSwitchNicTypeInternal**。

-   在 Hyper-v 子分区中运行的来宾操作系统。

    在此操作系统中公开的网络适配器使用[**NDIS\_交换机\_NIC\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)枚举值指定为**NdisSwitchNicTypeSynthetic**或**NdisSwitchNicTypeEmulated**。

如果[oid\_SWITCH\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)的 oid 查询请求完成且状态为 NDIS\_状态\_成功，则转发扩展可以通过检查每个[**NDIS\_开关来确定 VF 分配\_NIC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)返回的数组中的参数结构。 如果 Ndis\_交换机的**VFAssigned**成员 **\_nic\_参数**结构设置为**TRUE**，则对应于 NDIS\_交换机的网络适配器 **\_NIC\_参数**将结构分配给 VF。

转发扩展可以通过发出**NDIS\_状态\_交换机\_端口来删除分配，\_删除\_VF**状态指示。 在这种情况下，转发扩展必须将[**ndis\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)的**DestinationPortId**成员设置为 Ndis\_switch 的**PortId**成员的值[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构。

有关如何 **\_交换机\_\_端口发出 ndis\_状态**的详细信息，请参阅\_VF 状态指示\_[交换机\_**端口\_删除\_VF**状态指示](#issuing)。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_交换机\_NIC\_状态**](ndis-status-switch-nic-status.md)

[**NDIS\_交换机\_NIC\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)

[ **\_NIC\_参数的 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NDIS\_交换机\_NIC\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)

[OID\_交换机\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)

 

 




