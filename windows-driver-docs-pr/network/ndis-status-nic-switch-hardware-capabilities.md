---
title: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 状态指示到 NDIS 和已更改的网络适配器中的 NIC 交换机的硬件功能的基础驱动程序。
ms.assetid: 21B326EC-22CC-4E41-895F-457971202C0B
ms.date: 08/08/2017
keywords: -NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 49b911a31a2b9df397db61c1e3462f67a11bd1bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576012"
---
# <a name="ndisstatusnicswitchhardwarecapabilities"></a>NDIS\_状态\_NIC\_交换机\_硬件\_功能


**NDIS\_状态\_NIC\_交换机\_硬件\_功能**状态指示到 NDIS 和基础驱动程序的 NIC 的硬件功能中的网络适配器的交换机已更改。 这些功能包括由 INF 文件设置或通过当前已禁用的硬件功能**高级**属性页。

状态指示是通过微型端口驱动程序的网络适配器的 PCI Express (PCIe) 物理函数 (PF)。 PF 微型端口驱动程序在 HYPER-V 父分区的管理操作系统中运行。

<a name="remarks"></a>备注
-------

PF 微型端口驱动程序必须发出**NDIS\_状态\_NIC\_交换机\_硬件\_功能**状态指示只要它检测到的更改网络适配器上的 NIC 交换机的硬件功能。 当以下条件之一为 true 时，无法更改这些功能：

-   启用或禁用通过管理应用程序开发的独立硬件供应商 (IHV) NIC 交换机硬件功能。

-   适用于属于负载均衡由 MUX 中间驱动程序管理的故障转移 (LBFO) 团队的一个或多个网络适配器更改 NIC 的交换机的硬件功能。 有关详细信息，请参阅[NDIS MUX 中间驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566498)。

当 PF 微型端口驱动程序发出**NDIS\_状态\_NIC\_交换机\_硬件\_功能**状态指示，它必须执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_NIC\_切换\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)与网络适配器的 NIC 交换机的硬件功能的结构.
2.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构如下所示：

    -   **StatusCode**成员必须设置为**NDIS\_状态\_NIC\_开关\_硬件\_功能**。

    -   **StatusBuffer**成员必须设置为指向指针[ **NDIS\_NIC\_开关\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。 此结构包含 NIC 交换机的硬件功能。

    -   **StatusBufferSize**成员必须设置为 sizeof ([**NDIS\_NIC\_开关\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583))。

3.  PF 微型端口驱动程序通过调用发出状态通知[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)。 该驱动程序必须传递一个指向[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构*StatusIndication*参数。

过量驱动程序可以使用**NDIS\_状态\_NIC\_切换\_硬件\_功能**状态指示，以确定当前已启用的 NIC 开关网络适配器的功能。 或者，这些驱动程序还可以颁发的 OID 查询请求[OID\_NIC\_交换机\_硬件\_功能](oid-nic-switch-hardware-capabilities.md)在任何时候获取这些功能。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_NIC\_交换机\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[OID\_NIC\_交换机\_硬件\_功能](oid-nic-switch-hardware-capabilities.md)

 

 




