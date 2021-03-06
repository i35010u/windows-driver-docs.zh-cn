---
title: OID_NIC_SWITCH_DELETE_SWITCH
description: NDIS (OID 发出对象标识符) 将 OID_NIC_SWITCH_DELETE_SWITCH 请求从网络适配器中删除 NIC 交换机。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_DELETE_SWITCH 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b0edb36920e4ad68d45d74fc4a97536addce735
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248557"
---
# <a name="oid_nic_switch_delete_switch"></a>OID \_ NIC \_ 交换机 \_ 删除 \_ 开关


NDIS (OID 发出对象标识符) 设置 OID \_ nic 交换机的请求 \_ \_ \_ 从网络适配器中删除 nic 交换机。

NDIS 将此 OID 集请求颁发给网络适配器 PCI Express (PCIe 的微型端口驱动程序，) 物理功能 (PF) 。 对于支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PF 小型端口驱动程序，需要此 OID 集请求。

**注意**  过量驱动程序（如协议或筛选器驱动程序）无法向 PF 微型端口驱动程序发出此 OID 方法请求。

 

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ NIC \_ SWITCH \_ DELETE \_ SWITCH \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)结构的指针。

<a name="remarks"></a>备注
-------

Oid \_ nic 交换机删除交换机的 oid 集请求 \_ \_ \_ 删除先前通过 oid [ \_ nic \_ 交换机 \_ CREATE \_ SWITCH](oid-nic-switch-create-switch.md)的 oid 方法请求创建的 NIC 交换机。

接收到 oid NIC 交换机删除开关的 OID 方法请求时 \_ \_ \_ \_ ，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的软件资源。 但是，在调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 时，驱动程序只能释放 NIC 交换机的硬件资源。

    有关静态 NIC 交换机创建的详细信息，请参阅 [静态创建 Nic 交换机](./static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的硬件和软件资源。

    有关动态 NIC 交换机创建的详细信息，请参阅 [动态创建 Nic 交换机](./dynamic-creation-of-a-nic-switch.md)。

3.  如果 PF 微型端口驱动程序支持动态创建，并且已删除所有 NIC 交换机，则驱动程序必须通过调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)禁用适配器上的虚拟化。 若要禁用虚拟化，网络适配器必须将 *EnableVirtualization* 参数设置为 FALSE，将 *NumVFs* 参数设置为零。

    [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 清除 **NumVFs** 成员，并且 VF 在网络适配器的 PF 的 PCI 配置空间中的 sr-iov 扩展功能结构中 **启用** 位。

    **注意** 如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则在调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，它必须仅调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 。

     

有关详细信息，请参阅 [删除 NIC 交换机](./deleting-a-nic-switch.md)。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数为此请求返回以下值之一：

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
<td><p>微型端口驱动程序将异步完成请求。 当微型端口驱动程序完成所有处理后，它必须通过调用 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete" data-raw-source="[&lt;strong&gt;NdisMOidRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)"><strong>NdisMOidRequestComplete</strong></a> 函数来成功请求，同时传递 <strong>NDIS_STATUS_SUCCESS</strong> 的 <em>状态</em> 参数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NDIS_STATUS_NOT_ACCEPTED</strong></p></td>
<td><p>正在重置微型端口驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_REQUEST_ABORTED</strong></p></td>
<td><p>微型端口驱动程序已停止处理请求。 例如，NDIS 称为 <a href="/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset" data-raw-source="[&lt;em&gt;MiniportResetEx&lt;/em&gt;](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)"><em>MiniportResetEx</em></a> 函数。</p></td>
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
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)"><strong>NDIS_NIC_SWITCH_DELETE_SWITCH_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p><strong>NDIS_STATUS_INVALID_LENGTH</strong></p></td>
<td><p>信息缓冲区太小。 NDIS 设置 <strong>数据。SET_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ NIC \_ 交换机 \_ 删除 \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ NIC \_ 交换机 \_ 创建 \_ 开关](oid-nic-switch-create-switch.md)

[OID \_ NIC \_ 交换机 \_ 删除 \_ VPORT](oid-nic-switch-delete-vport.md)

[OID \_ NIC \_ 交换机 \_ 免费 \_ VF](oid-nic-switch-free-vf.md)

