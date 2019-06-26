---
title: NDIS_STATUS_SWITCH_PORT_REMOVE_VF
description: 转发扩展，若要删除虚拟机 (VM) 网络适配器和 PCI Express (PCIe) 的虚拟函数 (VF) 之间的绑定的 HYPER-V 可扩展交换机颁发 NDIS_STATUS_SWITCH_PORT_REMOVE_VF 状态指示。
ms.assetid: D6A52183-C9C6-4F0B-9E25-6C5C16CBEFFE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_SWITCH_PORT_REMOVE_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d8e25b138206972889adcad286537bbd3028e9d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385071"
---
# <a name="ndisstatusswitchportremovevf"></a>NDIS\_状态\_交换机\_端口\_删除\_VF


**NDIS\_状态\_切换\_端口\_删除\_VF**状态指示颁发的转发扩展删除绑定的 HYPER-V 可扩展交换机虚拟机 (VM) 之间的网络适配器和 PCI Express (PCIe) 的虚拟函数 (VF)。 VF 公开和受支持的单个根 I/O 虚拟化 (SR-IOV) 接口的基础物理网络适配器。

为了颁发**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示转发扩展必须封装中的指示[**NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构和问题[ **NDIS\_状态\_交换机\_NIC\_状态**](ndis-status-switch-nic-status.md)状态指示。

此过程的详细信息，请参阅[颁发的指导原则**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示](#issuing).

<a name="remarks"></a>备注
-------

创建并分配的基础物理适配器支持 SR-IOV 接口 PCIe VF。 创建后，将附加虚拟化堆栈，或*分配*，VF 到 HYPER-V 子分区。 此分区中运行来宾操作系统公开绑定到的 VF 基础 SR-IOV 物理适配器的虚拟机 (VM) 网络适配器。

在虚拟和物理网络适配器分配后, 直接 VF 和 VM 网络适配器之间路由数据包。 但是，因为数据包传递不涉及可扩展交换机，则可扩展交换机端口策略不应用这些数据包。 这包括端口策略的访问控制列表 (Acl) 和服务质量 (QoS)。

转发扩展的可扩展交换机可以通过发出删除分配到子分区 VF **NDIS\_状态\_切换\_端口\_删除\_VF**状态指示。 此指示会导致将通过可扩展的交换机端口而不是直接在 VM 网络适配器和 VF 基础 SR-IOV 物理适配器之间发送的数据包。 这样，可扩展交换机端口策略应用于接收或通过可扩展交换机端口发送的数据包。

当转发扩展，可以**NDIS\_状态\_切换\_端口\_删除\_VF**状态指示，它指定到可扩展交换机端口VM 网络适配器已连接。

有关转发扩展的可扩展交换机的详细信息，请参阅[转发扩展](https://docs.microsoft.com/windows-hardware/drivers/network/forwarding-extensions)。

### <a href="" id="issuing"></a>用于颁发 NDIS 准则\_状态\_交换机\_端口\_删除\_VF 状态指示

为了颁发**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示转发扩展必须执行以下步骤：

1.  转发扩展初始化[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构**NDIS\_状态\_开关\_端口\_删除\_VF**指示。 为此可能转发扩展设置的以下成员**NDIS\_状态\_指示**结构：

    -   **StatusCode**成员必须设置为**NDIS\_状态\_开关\_端口\_删除\_VF**。

    -   **StatusBuffer**成员必须设置为**NULL**。

    -   **StatusBufferSize**必须设置为零。

2.  转发扩展初始化[ **NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构。 若要删除的 VF 分配，转发扩展必须按以下方式设置的成员：

    -   **DestinationPortId**成员必须设置为 VM 网络适配器连接到可扩展的交换机端口的标识符。

    -   **DestinationNicIndex**成员必须设置为连接到指定的端口的 VM 网络适配器的索引值。

    -   **SourcePortId**成员必须设置为**NDIS\_交换机\_默认\_端口\_ID**。

    -   **SourceNicIndex**成员必须设置为**NDIS\_交换机\_默认\_NIC\_索引**。

    -   **StatusIndication**成员必须设置为的地址[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构**NDIS\_状态\_交换机\_端口\_删除\_VF**指示。

3.  转发扩展初始化[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构[ **NDIS\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)指示。 为此可能转发扩展设置的以下成员**NDIS\_状态\_指示**结构：

    -   **StatusCode**成员必须设置为[ **NDIS\_状态\_开关\_NIC\_状态**](ndis-status-switch-nic-status.md)。

    -   **StatusBuffer**成员必须设置为的地址[ **NDIS\_开关\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构。

    -   **StatusBufferSize**必须设置为的长度，以字节为单位的[ **NDIS\_开关\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构并[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构**NDIS\_状态\_交换机\_端口\_删除\_VF**指示。

4.  转发扩展必须调用[ *ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)递增引用计数器，用于 VM 网络适配器。 如果*ReferenceSwitchNic*不会完成使用 NDIS\_状态\_成功后，转发扩展必须转发的状态指示。

    **请注意**  如果转发扩展已收到[OID\_交换机\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)设置请求的 VM 适配器，它不能调用[*ReferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)也将转发的状态指示。

     

5.  转发扩展将调用[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)转发[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)到过量可扩展交换机驱动程序堆栈中的扩展。 当转发扩展调用此函数时，它会设置*StatusIndication*指向的指针参数**NDIS\_状态\_指示**结构[**NDIS\_状态\_交换机\_NIC\_状态**](ndis-status-switch-nic-status.md)指示。

6.  之后[ **NdisFIndicateStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)返回，则转发扩展必须调用[ *DereferenceSwitchNic* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)要递减VM 网络适配器的引用计数器。

**请注意**  转发扩展必须遵循针对每个删除转发扩展的取景器分配的上一步骤。

 

有关转发扩展转发状态的指示方式的详细信息，请参阅[筛选器模块状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/filter-module-status-indications)。

### <a name="guidelines-for-determining-vf-assignments"></a>指导原则来确定 VF 分配

转发扩展可以通过发出 OID 查询请求的枚举的虚拟网络适配器的当前 VF 分配[OID\_交换机\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)。 此请求将返回[ **NDIS\_交换机\_NIC\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_array)结构，其中包含的数组[ **NDIS\_交换机\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构。 每个**NDIS\_交换机\_NIC\_参数**结构指定的参数的公开的网络适配器中的以下环境：

-   管理操作系统的 HYPER-V 父分区中运行。

    在此操作系统中公开的网络适配器指定与[ **NDIS\_交换机\_NIC\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_nic_type)枚举值的**NdisSwitchNicTypeExternal**或**NdisSwitchNicTypeInternal**。

-   来宾操作系统运行的 HYPER-V 子分区中。

    在此操作系统中公开的网络适配器指定与[ **NDIS\_交换机\_NIC\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_nic_type)枚举值的**NdisSwitchNicTypeSynthetic**或**NdisSwitchNicTypeEmulated**。

如果 OID 查询请求的则[OID\_交换机\_NIC\_数组](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)完成状态为 NDIS\_状态\_成功后，转发扩展可以决定 VF通过检查每个分配[ **NDIS\_交换机\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)返回的数组中的结构。 如果**VFAssigned**的成员**NDIS\_交换机\_NIC\_参数**结构设置为**TRUE**，网络适配器对应于**NDIS\_交换机\_NIC\_参数**结构分配给 VF。

转发扩展可以通过发出删除分配**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示。 在这种情况下，必须设置转发扩展**DestinationPortId**的成员[ **NDIS\_开关\_NIC\_状态\_指示** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)的值**PortId**的成员[ **NDIS\_交换机\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构。

有关详细信息如何发出**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示，请参阅[颁发的准则**NDIS\_状态\_交换机\_端口\_删除\_VF**状态指示](#issuing)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatestatus)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_交换机\_NIC\_状态**](ndis-status-switch-nic-status.md)

[**NDIS\_SWITCH\_NIC\_ARRAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_array)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NDIS\_SWITCH\_NIC\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_switch_nic_type)

[OID\_SWITCH\_NIC\_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)

 

 




