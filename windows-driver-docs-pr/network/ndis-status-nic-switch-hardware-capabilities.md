---
title: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 状态向 NDIS 和过量驱动程序指示网络适配器中 NIC 交换机的硬件功能已更改。
ms.assetid: 21B326EC-22CC-4E41-895F-457971202C0B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 978b74796c3f5fd45f4f1266f66488e532c60958
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842783"
---
# <a name="ndis_status_nic_switch_hardware_capabilities"></a>\_NIC\_交换机\_硬件\_功能的 NDIS\_状态


**Ndis\_状态\_NIC\_交换机\_硬件\_功能**状态向 NDIS 和过量驱动程序指示网络适配器中 NIC 交换机的硬件功能已更改。 这些功能包括 INF 文件设置当前禁用的硬件功能，或通过 "**高级**属性" 页禁用的硬件功能。

状态指示由网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序进行。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行。

<a name="remarks"></a>备注
-------

每当检测到网络适配器上的 NIC 交换机的硬件功能发生变化时，PF 微型端口驱动程序必须 **\_NIC 上发出 NDIS\_状态 nic\_交换机\_硬件\_功能**状态指示。 当满足以下条件之一时，这些功能可能会更改：

-   通过独立硬件供应商（IHV）开发的管理应用程序启用或禁用 NIC 交换机硬件功能。

-   NIC 交换机硬件功能对于属于某个 MUX 中间驱动程序管理的负载平衡故障转移（LBFO）团队的一个或多个网络适配器发生变化。 有关详细信息，请参阅[NDIS MUX 中间驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)。

当 PF 微型端口驱动程序发出**NDIS\_状态时\_NIC\_交换机\_硬件\_功能**状态指示，必须执行以下步骤：

1.  微型端口驱动程序使用网络适配器的 NIC 交换机的硬件功能初始化[**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。
2.  微型端口驱动程序通过以下方式初始化[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构：

    -   必须将**StatusCode**成员设置为**NDIS\_状态\_NIC\_交换机\_硬件\_功能**。

    -   **StatusBuffer**成员必须设置为指向[**NDIS\_NIC 的指针\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。 此结构包含 NIC 交换机的硬件功能。

    -   **StatusBufferSize**成员必须设置为 Sizeof （[**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)）。

3.  PF 微型端口驱动程序通过调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态通知。 驱动程序必须向*StatusIndication*参数传递指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。

过量驱动程序可以使用**NDIS\_状态\_NIC\_交换机\_硬件\_功能**状态指示来确定网络适配器上当前启用的 NIC 交换机功能。 此外，这些驱动程序还可以\_交换机\_NIC 发出 OID 查询请求， [\_硬件\_功能](oid-nic-switch-hardware-capabilities.md)随时获取这些功能。

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
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_NIC\_交换机\_硬件\_功能](oid-nic-switch-hardware-capabilities.md)

 

 




