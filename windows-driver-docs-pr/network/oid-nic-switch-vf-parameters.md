---
title: OID_NIC_SWITCH_VF_PARAMETERS
description: 覆盖驱动程序或用户模式应用程序发出对象标识符 (OID) 方法请求 OID_NIC_SWITCH_VF_PARAMETERS，以便在网络适配器上获取 PCI Express (PCIe) 虚拟函数 (虚拟函数的当前配置参数。
ms.assetid: DF08B0BA-6D86-4C4F-AC38-8A401F097925
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NIC_SWITCH_VF_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b7656e4bdb7ceb2eb75b016465f8fa02012f1dd9
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106014"
---
# <a name="oid_nic_switch_vf_parameters"></a>OID \_ NIC \_ 开关 \_ VF \_ 参数


覆盖驱动程序或用户模式应用程序会发出一个对象标识符 (OID) 方法请求 OID \_ NIC \_ SWITCH \_ VF \_ 参数，以便在网络适配器上获取 PCI Express (PCIe) 虚拟函数 (VF) 的当前配置参数。 只有具有通过 oid [ \_ nic \_ 交换机 \_ \_ ](oid-nic-switch-allocate-vf.md) 的 oid 方法请求分配的资源的 VFs 才能通过 OID \_ nic \_ 开关 \_ VF 参数的 oid 方法请求进行查询 \_ 。

NDIS \_ \_ \_ \_ 为微型端口驱动程序处理 oid NIC 交换机 VF 参数的 oid 方法请求。

进行 OID 方法请求时， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 开关 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的指针。

<a name="remarks"></a>注解
-------

过量驱动程序或用户模式应用程序通过将[**NDIS \_ NIC \_ 开关 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的**VFId**成员设置为 VF 的标识符来指定要查询的 VF。 过量驱动程序或应用程序通过以下方式之一获取 VF 标识符：

-   通过发出 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VFS](oid-nic-switch-enum-vfs.md)的 oid 方法请求。

    如果此 OID 请求成功完成，则过量驱动程序或用户模式应用程序将收到网络适配器上分配的所有 VFs 的列表。 列表中的每个元素都是一个 [**NDIS \_ NIC \_ 交换机 \_ vf \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info) 结构，其中包含由 **VFId** 成员指定的 VF 标识符。

-   通过发出 Oid NIC 交换机的 OID 方法请求 [ \_ \_ \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)。

    如果此 OID 请求成功完成，则过量驱动程序会在返回的[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的**VFID**成员中接收新创建的 VF 的标识符。

    **注意**   只有过量驱动程序才能以这种方式获取 VF 标识符。

     

成功从 OID 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的指针。 此结构包含指定的 VF 的配置参数。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理 \_ \_ \_ 适用于微型端口驱动程序的 oid NIC 开关 VF 参数的 oid 方法请求 \_ ，并为 oid \_ NIC \_ 开关 \_ vf 参数的 oid 方法请求返回以下状态代码 \_ 。

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
<td><p>请求已成功完成。 <strong>InformationBuffer</strong>成员指向<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>微型端口驱动程序不支持 (SR-IOV) 接口的单个根 i/o 虚拟化，或者未启用使用该接口。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>结构的一个或多个成员的值无效。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度小于 sizeof (<a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VF_PARAMETERS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)"><strong>NDIS_NIC_SWITCH_VF_PARAMETERS</strong></a>) 。 NDIS 设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区太短。 NDIS 设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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

## <a name="see-also"></a>请参阅


****
[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID \_ NIC \_ 交换机 \_ 分配 \_ VF](oid-nic-switch-allocate-vf.md)

[OID \_ NIC \_ 交换机 \_ 枚举 \_ VFS](oid-nic-switch-enum-vfs.md)

[**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)

[OID \_ NIC \_ 开关 \_ VF \_ 参数](oid-nic-switch-vf-parameters.md)

