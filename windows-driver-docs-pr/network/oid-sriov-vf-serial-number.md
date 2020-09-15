---
title: OID_SRIOV_VF_SERIAL_NUMBER
description: 过量驱动程序发出对象标识符 (OID) 查询请求 OID_SRIOV_VF_SERIAL_NUMBER，以确定 PCI Express (PCIe) 虚拟函数 (虚拟) 网络适配器的序列号。
ms.assetid: C4D04C96-94FA-4E01-839C-A9C5026D7AE5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SRIOV_VF_SERIAL_NUMBER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e16e93d2714dfabd0a89ae2cef0e8356d9e77f52
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104974"
---
# <a name="oid_sriov_vf_serial_number"></a>OID \_ SRIOV \_ VF \_ 序列 \_ 号


过量驱动程序) OID SRIOV VF 序列号请求 (OID 发出对象 \_ 标识符 \_ \_ \_ ，以确定 PCI Express (PCIe) 虚函数的序列号 (网络适配器) VF。 此虚拟网络适配器显示在 VF 附加到的 Hyper-v 子分区的来宾操作系统中。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ SRIOV \_ VF \_ 序列 \_ 号 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)结构的指针。

<a name="remarks"></a>备注
-------

过量驱动程序使用序列号将 VF 网络适配器映射到物理网络适配器上的 VF 的实例。 序列号是由虚拟化堆栈生成的，在通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](oid-nic-switch-allocate-vf.md)的 oid 集请求分配 vf 的资源之前。

### <a name="return-status-codes"></a>返回状态代码

NDIS \_ \_ \_ \_ 为微型端口驱动程序处理 oid SRIOV VF 序列号请求的 oid 查询请求。 将不会向此 OID 请求颁发驱动程序。

当 NDIS 处理 OID \_ SRIOV \_ VF \_ 序列 \_ 号请求时，它将返回以下状态代码之一。

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
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
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
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ SRIOV \_ VF \_ 序列 \_ 号 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_vf_serial_number_info)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

