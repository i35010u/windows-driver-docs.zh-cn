---
title: OID_NIC_SWITCH_CREATE_SWITCH
description: NDIS) 方法请求 (OID 发出对象标识符，OID_NIC_SWITCH_CREATE_SWITCH 在网络适配器上创建 NIC 交换机。
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CREATE_SWITCH 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d13080d0b743b634b525ec40a4741e3a6ee2fc53
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209659"
---
# <a name="oid_nic_switch_create_switch"></a>OID \_ NIC \_ 交换机 \_ 创建 \_ 开关


NDIS)  (OID 发出对象标识符，oid \_ NIC \_ 交换机 \_ create \_ 开关用于在网络适配器上创建 NIC 交换机。 当它处理此 OID 请求时，微型端口驱动程序为适配器上的 NIC 交换机分配资源。

NDIS 将此 OID 方法请求颁发给网络适配器 PCI Express (PCIe 的微型端口驱动程序，) 物理功能 (PF) 。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 方法请求。

**注意**   过量驱动程序（如协议或筛选器驱动程序）无法发出 oid \_ NIC \_ 交换机 \_ CREATE \_ 切换到 PF 微型端口驱动程序的 oid 方法请求。

 

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构的指针。

<a name="remarks"></a>备注
-------

接收到 oid NIC 交换机 CREATE SWITCH 的 OID 方法请求时 \_ \_ \_ \_ ，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态交换机创建和配置，它将在 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时创建 NIC 交换机。 当驱动程序处理此 OID 请求时，它必须验证 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构中的配置参数。 参数必须与驱动程序在调用 *MiniportInitializeEx*期间使用的参数相同。 如果不是这样，则驱动程序必须使 OID 请求失败。

    有关详细信息，请参阅 [创建 NIC 交换机的静态](./static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态交换机创建和配置，则驱动程序必须验证 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构的配置值，并根据这些值创建 NIC 交换机。

    有关详细信息，请参阅 [动态创建 NIC 交换机](./dynamic-creation-of-a-nic-switch.md)。

3.  PF 小型端口驱动程序必须为 NIC 交换机上的默认 VPort 分配必要的硬件和软件资源。

    **注意**   默认 VPort 始终通过 oid \_ nic 交换机 CREATE 开关的 oid 请求创建 \_ \_ \_ ，并通过 oid [ \_ nic \_ 交换机 \_ 删除 \_ 开关](oid-nic-switch-delete-switch.md)的 oid 请求删除。 Oid [ \_ nic \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md) 和 [oid \_ nic \_ 交换机 \_ DELETE \_ VPORT](oid-nic-switch-delete-vport.md) 的 Oid 请求用于在 NIC 交换机上创建和删除非默认 VPorts。

     

4.  支持动态交换机创建和配置的 PF 微型端口驱动程序必须通过调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)在交换机上启用 sr-iov 虚拟化。 此调用配置 **NumVFs** 成员，并且在适配器 PCI Express (PCIe) 配置空间的 Sr-iov 扩展功能结构中 **启用 "VF** "。

    有关 SR-IOV 配置空间的详细信息，请参阅 PCI-SIG [单根 I/o 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742) 规范。

    **注意**   如果 PF 微型端口驱动程序支持静态交换机创建，则在调用[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时，它将启用 sr-iov 虚拟化。

     

如果 PF 微型端口驱动程序成功完成 OID \_ NIC 交换机 CREATE SWITCH 的 oid 方法请求 \_ \_ \_ ，则允许执行以下操作：

-   可以通过 oid [ \_ nic \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)的 oid 方法请求，在 NIC 交换机上分配 VFs。

-   可以通过 oid [ \_ nic \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md)的 oid 方法请求在 NIC 交换机上创建非默认 VPorts。

有关如何处理此 OID 请求的详细信息，请参阅 [处理 oid \_ NIC \_ 交换机 \_ CREATE \_ SWITCH 请求](./handling-the-oid-nic-switch-create-switch-request.md)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 OID \_ NIC \_ 交换机 \_ 创建开关的 oid 方法请求返回以下状态代码之一 \_ 。

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
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF 微型端口驱动程序不支持 SR-IOV 接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>) 。 PF 微型端口驱动程序必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
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
[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](oid-nic-switch-create-vport.md)

 

