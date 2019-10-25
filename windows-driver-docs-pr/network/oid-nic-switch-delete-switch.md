---
title: OID_NIC_SWITCH_DELETE_SWITCH
description: NDIS 发出 OID_NIC_SWITCH_DELETE_SWITCH 的对象标识符（OID）设置请求，以从网络适配器中删除 NIC 交换机。
ms.assetid: 5785B30F-B67F-4D5A-A93A-243D33B9CAE8
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_DELETE_SWITCH 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7199d00167497b89a4f4a92d06f72d872289aaaf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844093"
---
# <a name="oid_nic_switch_delete_switch"></a>OID\_NIC\_交换机\_DELETE\_开关


NDIS 发出 OID\_NIC 的对象标识符（OID）设置请求\_交换机\_DELETE\_开关从网络适配器中删除 NIC 交换机。

NDIS 将此 OID 集请求颁发给网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。 支持单一根 i/o 虚拟化（SR-IOV）接口的 PF 微型端口驱动程序需要此 OID 集请求。

**请注意**  过量驱动程序（如协议或筛选器驱动程序）无法向 PF 微型端口驱动程序发出此 OID 方法请求。

 

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)的指针，该指针\_\_DELETE\_参数结构。

<a name="remarks"></a>备注
-------

Oid\_NIC\_交换机\_DELETE\_开关的 OID 设置将删除先前通过 oid 的 OID 方法请求创建的 NIC 交换机\_\_\_\_[创建开关](oid-nic-switch-create-switch.md)。

当接收到 oid\_NIC 的 OID 方法请求时\_交换机\_DELETE\_开关，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的软件资源。 但是，在调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，驱动程序只能释放 NIC 交换机的硬件资源。

    有关静态 NIC 交换机创建的详细信息，请参阅[静态创建 Nic 交换机](https://docs.microsoft.com/windows-hardware/drivers/network/static-creation-of-a-nic-switch)。

2.  如果 PF 微型端口驱动程序支持动态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的硬件和软件资源。

    有关动态 NIC 交换机创建的详细信息，请参阅[动态创建 Nic 交换机](https://docs.microsoft.com/windows-hardware/drivers/network/dynamic-creation-of-a-nic-switch)。

3.  如果 PF 微型端口驱动程序支持动态创建，并且已删除所有 NIC 交换机，则驱动程序必须通过调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)禁用适配器上的虚拟化。 若要禁用虚拟化，网络适配器必须将*EnableVirtualization*参数设置为 FALSE，将*NumVFs*参数设置为零。

    [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)清除**NumVFs**成员，并且 VF 在网络适配器的 PF 的 PCI 配置空间中的 sr-iov 扩展功能结构中**启用**位。

    **请注意**  如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则在调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，它必须仅调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 。

     

有关详细信息，请参阅[删除 NIC 交换机](https://docs.microsoft.com/windows-hardware/drivers/network/deleting-a-nic-switch)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数为此请求返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>微型端口驱动程序已成功完成请求。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_PENDING</strong></p></td>
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a>函数（为<em>STATUS</em>参数传递<strong>NDIS_STATUS_SUCCESS</strong> ）成功执行请求。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a>函数。</p></td>
</tr>
</tbody>
</table>

 

NDIS 为此请求返回以下状态代码之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>NDIS_STATUS_SUCCESS</strong></p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_NOT_SUPPORTED</strong></p></td>
<td><p>PF 微型端口驱动程序不支持 SR-IOV 接口，或者没有启用使用接口。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_FILE_NOT_FOUND</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS</strong></a>结构中的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太小。 NDIS 设置<strong>数据。SET_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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
[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[ **\_交换机\_\_\_的 NDIS 交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)

[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)

[OID\_NIC\_交换机\_创建\_交换机](oid-nic-switch-create-switch.md)

[OID\_NIC\_交换机\_DELETE\_VPORT](oid-nic-switch-delete-vport.md)

[OID\_NIC\_交换机\_免费\_VF](oid-nic-switch-free-vf.md)

 

 




