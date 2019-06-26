---
title: OID_SRIOV_VF_SERIAL_NUMBER
description: 基础驱动程序发出的对象标识符 (OID) 查询请求的 OID_SRIOV_VF_SERIAL_NUMBER 来确定 PCI Express (PCIe) 的虚拟函数 (VF) 网络适配器的序列号。
ms.assetid: C4D04C96-94FA-4E01-839C-A9C5026D7AE5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_SERIAL_NUMBER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a0f4f753b5475ec1f564b4064be24801f4df5dce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373901"
---
# <a name="oidsriovvfserialnumber"></a>OID\_SRIOV\_VF\_SERIAL\_NUMBER


基础驱动程序将发出对象标识符 (OID) 查询请求的 OID\_SRIOV\_VF\_串行\_编号，以确定 PCI Express (PCIe) 的虚拟函数 (VF) 网络适配器的序列号。 此虚拟网络适配器的 HYPER-V 子分区取景器附加到来宾操作系统中公开。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_SRIOV\_VF\_串行\_号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)结构。

<a name="remarks"></a>备注
-------

基础驱动程序使用序列号映射到的物理网络适配器上 VF 实例 VF 网络适配器。 之前通过 OID 集请求的分配 VF 的资源，由虚拟化堆栈生成的序列号[OID\_NIC\_交换机\_分配\_VF](oid-nic-switch-allocate-vf.md)。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 OID 查询请求的 OID\_SRIOV\_VF\_串行\_数字请求微型端口驱动程序。 驱动程序将不会颁发此 OID 请求。

NDIS 时处理 OID\_SRIOV\_VF\_串行\_请求数，它将返回一个下面的状态代码。

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
<td><p>微型端口驱动程序不支持的单个根 I/O 虚拟化 (SR-IOV) 接口，或未启用要使用的界面。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 集<strong>数据。QUERY_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>请求由于其他原因而失败。</p></td>
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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SRIOV\_VF\_SERIAL\_NUMBER\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)

[OID\_NIC\_SWITCH\_ALLOCATE\_VF](oid-nic-switch-allocate-vf.md)

 

 




