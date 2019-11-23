---
title: OID_NIC_SWITCH_CREATE_SWITCH
description: NDIS 发出 OID_NIC_SWITCH_CREATE_SWITCH 的对象标识符（OID）方法请求，以便在网络适配器上创建 NIC 交换机。
ms.assetid: 16FFC6A4-11A6-45A1-ABCF-8C1EBE3FD953
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_CREATE_SWITCH 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 185eb66205c98cef3e6df73e078db59395d8c8bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844100"
---
# <a name="oid_nic_switch_create_switch"></a>OID\_NIC\_交换机\_创建\_交换机


NDIS 发出 OID\_NIC 的对象标识符（OID）方法请求\_交换机\_创建\_交换机，以便在网络适配器上创建 NIC 交换机。 当它处理此 OID 请求时，微型端口驱动程序为适配器上的 NIC 交换机分配资源。

NDIS 将此 OID 方法请求颁发给网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 对于支持单个根 i/o 虚拟化（SR-IOV）接口的 PF 小型端口驱动程序，此 OID 方法请求是必需的。

**请注意**  过量驱动程序（如协议或筛选器驱动程序）不能\_\_NIC 发出 oid 方法请求，\_创建\_交换机到 PF 微型端口驱动程序。

 

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_SWITCH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。

<a name="remarks"></a>备注
-------

当接收到 oid\_NIC 的 OID 方法请求时\_交换机\_创建\_交换机，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态交换机创建和配置，它将在 NDIS 调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时创建 NIC 交换机。 当驱动程序处理此 OID 请求时，它必须验证 NDIS\_NIC 中的配置参数[ **\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 参数必须与驱动程序在调用*MiniportInitializeEx*期间使用的参数相同。 如果不是这样，则驱动程序必须使 OID 请求失败。

    有关详细信息，请参阅[创建 NIC 交换机的静态](https://docs.microsoft.com/windows-hardware/drivers/network/static-creation-of-a-nic-switch)。

2.  如果 PF 微型端口驱动程序支持动态交换机创建和配置，则驱动程序必须验证[**NDIS\_NIC 的配置值\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构，并根据这些值创建 NIC 交换机。

    有关详细信息，请参阅[动态创建 NIC 交换机](https://docs.microsoft.com/windows-hardware/drivers/network/dynamic-creation-of-a-nic-switch)。

3.  PF 小型端口驱动程序必须为 NIC 交换机上的默认 VPort 分配必要的硬件和软件资源。

    **请注意**  默认 VPort 始终通过 oid 的 oid 请求\_NIC\_SWITCH\_创建\_交换机，并通过 oid\_\_\_\_[DELETE](oid-nic-switch-delete-switch.md)交换机的 oid 请求删除。 [Oid\_nic 的 oid 请求\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)和[OID\_nic\_交换机\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)用于在 nic 交换机上创建和删除非默认 VPorts。

     

4.  支持动态交换机创建和配置的 PF 微型端口驱动程序必须通过调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)在交换机上启用 sr-iov 虚拟化。 此调用在适配器的 PCI Express （PCIe）配置空间的 SR-IOV 扩展功能结构中配置**NumVFs**成员和**VF 启用**位。

    有关 SR-IOV 配置空间的详细信息，请参阅 PCI-SIG[单根 I/o 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)规范。

    **请注意**  如果 PF 微型端口驱动程序支持静态交换机创建，则在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时，它将启用 sr-iov 虚拟化。

     

如果 PF 微型端口驱动程序已成功完成 OID\_NIC 的 OID 方法请求\_交换机\_创建\_交换机，则允许执行以下操作：

-   可以通过 oid\_NIC 的 oid 方法请求[\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)来在 nic 交换机上分配 VFs。

-   可以通过 oid\_NIC 的 OID 方法请求[\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)创建非默认的 VPorts。

有关如何处理此 OID 请求的详细信息，请参阅[处理 oid\_NIC\_交换机\_创建\_切换请求](https://docs.microsoft.com/windows-hardware/drivers/network/handling-the-oid-nic-switch-create-switch-request)。

### <a name="return-status-codes"></a>返回状态代码

PF 多端口驱动程序为 oid\_NIC\_SWITCH\_创建\_开关返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof （<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)"><strong>NDIS_NIC_SWITCH_PARAMETERS</strong></a>）。 PF 微型端口驱动程序必须设置<strong>数据。METHOD_INFORMATION。</strong>将<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[ **\_交换机\_参数的 NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)

[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

 

 




