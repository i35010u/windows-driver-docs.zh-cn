---
title: NDIS_STATUS_SWITCH_PORT_REMOVE_VF
description: NDIS_STATUS_SWITCH_PORT_REMOVE_VF 状态指示是由 Hyper-v 可扩展交换机转发扩展颁发的，用于删除虚拟机 (VM) 网络适配器与 PCI Express (PCIe) 虚拟函数 (VF) 之间的绑定。
ms.assetid: D6A52183-C9C6-4F0B-9E25-6C5C16CBEFFE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_SWITCH_PORT_REMOVE_VF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cdb51529d85b47fb124120c61799cd1bacfbad95
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215524"
---
# <a name="ndis_status_switch_port_remove_vf"></a>NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF


**NDIS \_ 状态 \_ 交换机 \_ 端口 \_ 删除 \_ VF**状态指示是由 hyper-v 可扩展交换机转发扩展颁发的，用于删除虚拟机 (VM) 网络适配器与 PCI EXPRESS (PCIe) 虚函数 (VF) 之间的绑定。 VF 由支持单个根 i/o 虚拟化的基础物理网络适配器公开和支持 (SR-IOV) 接口。

为了发出 **ndis \_ 状态 \_ 切换端口，请 \_ \_ 删除 \_ VF** 状态指示，转发扩展必须将指示封装在 [**NDIS \_ 交换机 \_ nic \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构中，并发出 [**ndis \_ 状态 \_ 切换 \_ nic \_ 状态**](ndis-status-switch-nic-status.md) 状态指示。

有关此过程的详细信息，请参阅 [发出 **NDIS \_ 状态 \_ 交换机端口的 \_ 准则 \_ 删除 \_ VF** 状态指示](#issuing)。

<a name="remarks"></a>备注
-------

PCIe VF 由支持 SR-IOV 接口的基础物理适配器创建和分配。 创建后，虚拟化堆栈会将 VF 附加或 *分配*到 hyper-v 子分区。 在此分区中运行的来宾操作系统将公开一个 (VM) 网络适配器的虚拟机，该虚拟机绑定到基础 SR-IOV 物理适配器的 VF。

分配虚拟和物理网络适配器后，会直接在 VF 与 VM 网络适配器之间路由数据包。 但是，因为可扩展交换机不涉及数据包传递，所以可扩展交换机端口策略不会应用于这些数据包。 这包括访问控制列表 (Acl) 和服务质量 (QoS) 的端口策略。

可扩展的交换机转发扩展可以通过发出 **NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF** 状态指示来删除将 VF 分配给子分区。 此指示会导致数据包通过可扩展交换机端口发送，而不是直接在 VM 网络适配器和基础 SR-IOV 物理适配器的 VF 之间传输。 这允许将可扩展交换机端口策略应用到通过可扩展交换机端口接收或发送的数据包。

当转发扩展使 **NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF** 状态指示时，它将指定 VM 网络适配器连接到的可扩展交换机端口。

有关可扩展交换机转发扩展的详细信息，请参阅 [转发扩展](./forwarding-extensions.md)。

### <a name="guidelines-for-issuing-an-ndis_status_switch_port_remove_vf-status-indication"></a><a href="" id="issuing"></a>有关发出 NDIS \_ 状态 \_ 交换机端口的 \_ 准则 \_ 删除 \_ VF 状态指示

为了发出 **NDIS \_ 状态 \_ 切换端口，请 \_ \_ 删除 \_ VF** 状态指示，转发扩展必须执行以下步骤：

1.  转发扩展插件为**ndis \_ 状态 \_ 切换 \_ 端口 \_ \_ **初始化[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构，并删除 VF 指示。 对于这一指示，转发扩展会设置以下 **NDIS \_ 状态 \_ 指示** 结构的成员：

    -   **StatusCode**成员必须设置为**NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF**。

    -   **StatusBuffer**成员必须设置为**NULL**。

    -   **StatusBufferSize**必须设置为零。

2.  转发扩展插件初始化 [**NDIS \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构。 为了删除 VF 分配，转发扩展必须按以下方式设置成员：

    -   **DestinationPortId**成员必须设置为 VM 网络适配器连接到的可扩展交换机端口的标识符。

    -   **DestinationNicIndex**成员必须设置为连接到指定端口的 VM 网络适配器的索引值。

    -   **SourcePortId**成员必须设置为**NDIS \_ 交换机 \_ 默认 \_ 端口 \_ ID**。

    -   **SourceNicIndex**成员必须设置为**NDIS \_ SWITCH \_ DEFAULT \_ NIC \_ INDEX**。

    -   **StatusIndication**成员必须设置为 ndis 状态交换机端口的[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的地址，并** \_ \_ \_ \_ 删除 \_ VF**指示。

3.  转发扩展插件为[**ndis \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)指示初始化[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构。 对于此指示，转发扩展会设置以下 **NDIS \_ 状态 \_ 指示** 结构的成员：

    -   **StatusCode**成员必须设置为[**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](ndis-status-switch-nic-status.md)。

    -   **StatusBuffer**成员必须设置为[**NDIS \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的地址。

    -   必须将**StatusBufferSize**设置为[**ndis \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构的长度（以字节为单位），并将**ndis \_ 状态交换机端口的 \_ \_ \_ \_ ** [**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构删除 VF 指示。

4.  转发扩展必须调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 来递增 VM 网络适配器的引用计数器。 如果 *ReferenceSwitchNic* 未在 NDIS \_ 状态成功完成 \_ ，则转发扩展不能转发状态指示。

    **注意**   如果转发扩展插件已接收到 VM 适配器的[OID \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md)设置请求，则它不能调用[*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，也不能转发状态指示。

     

5.  转发扩展插件调用 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 将 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 转发到可扩展交换机驱动程序堆栈中的过量扩展。 当转发扩展插件调用此函数时，它会将*StatusIndication*参数设置为指向 ndis [** \_ 状态 \_ 切换 \_ NIC \_ 状态**](ndis-status-switch-nic-status.md)指示的**ndis \_ 状态 \_ 指示**结构的指针。

6.  [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)返回后，转发扩展必须调用[*DEREFERENCESWITCHNIC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)来减小 VM 网络适配器的引用计数器。

**注意**   对于正在删除转发扩展的每个 VF 分配，转发扩展必须遵循前面的步骤。

 

有关转发扩展转发状态指示的详细信息，请参阅 [筛选模块状态指示](./filter-module-status-indications.md)。

### <a name="guidelines-for-determining-vf-assignments"></a>确定 VF 分配的准则

转发扩展插件可以通过发出 [oid \_ 交换机 \_ NIC \_ 数组](./oid-switch-nic-array.md)的 oid 查询请求来枚举虚拟网络适配器的当前 VF 分配。 此请求返回 [**ndis \_ 交换机 \_ nic \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array) 结构，其中包含 [**ndis \_ 交换机 \_ nic \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构的数组。 每个 **NDIS \_ 交换机 \_ NIC \_ 参数** 结构指定在以下环境之一中公开的网络适配器的参数：

-   在 Hyper-v 父分区中运行的管理操作系统。

    在此操作系统中公开的网络适配器使用 [**NDIS \_ 交换机 \_ NIC \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type) 枚举值 **NdisSwitchNicTypeExternal** 或 **NdisSwitchNicTypeInternal**来指定。

-   在 Hyper-v 子分区中运行的来宾操作系统。

    在此操作系统中公开的网络适配器使用 [**NDIS \_ 交换机 \_ NIC \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type) 枚举值 **NdisSwitchNicTypeSynthetic** 或 **NdisSwitchNicTypeEmulated**来指定。

如果 [oid \_ 交换机 \_ NIC \_ 阵列](./oid-switch-nic-array.md) 的 oid 查询请求完成并且状态为 NDIS \_ 状态 \_ 成功，则转发扩展可以通过检查返回的数组中的每个 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构来确定 VF 分配。 如果**ndis \_ 交换机 \_ nic \_ 参数**结构的**VFAssigned**成员设置为**TRUE**，则将与**ndis \_ 交换机 \_ nic \_ 参数**结构相对应的网络适配器分配给 VF。

转发扩展可以通过发出 **NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF** 状态指示来删除分配。 在这种情况下，转发扩展必须将[**ndis \_ 交换机 \_ nic \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)的**DestinationPortId**成员设置为[**ndis \_ 交换机 \_ nic \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**PortId**成员的值。

若要详细了解如何发出 **ndis \_ 状态 \_ 交换机端口， \_ 请 \_ 删除 \_ vf** 状态指示，请参阅 [有关发出 **Ndis \_ 状态交换机端口的准则 \_ \_ \_ 删除 \_ vf** 状态指示](#issuing)。

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
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](ndis-status-switch-nic-status.md)

[**NDIS \_ 交换机 \_ NIC \_ 阵列**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_array)

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NDIS \_ 交换机 \_ NIC \_ 类型**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_switch_nic_type)

[OID \_ 交换机 \_ NIC \_ 阵列](./oid-switch-nic-array.md)

 

