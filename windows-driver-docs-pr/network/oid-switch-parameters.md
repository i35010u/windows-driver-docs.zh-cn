---
title: OID_SWITCH_PARAMETERS
description: Hyper-v 可扩展交换机扩展)  (OID 发出对象标识符，OID_SWITCH_PARAMETERS 获取可扩展交换机的配置数据。
ms.assetid: F2CA0BE5-ED21-4ACF-B26A-4F512D4B15C7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4cedcfd1f29fc3d02d2a6bc6e7305d8892cdd018
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423632"
---
# <a name="oid_switch_parameters"></a>OID \_ 开关 \_ 参数


Hyper-v 可扩展交换机扩展 (OID 发出对象标识符) 请求 OID \_ 开关 \_ 参数以获取可扩展交换机的配置数据。

如果 OID 查询请求成功完成， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构的指针。

<a name="remarks"></a>备注
-------

当扩展处理返回的 [**ndis \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters) 结构时，它不能假定 **ndis \_ 开关 \_ 参数** 结构的各个字符串成员（如 **SwitchName**）都以 null 结尾。 这些字符串成员的数据类型由 [**IF \_ 计数 \_ 字符串**](/windows/win32/api/ifdef/ns-ifdef-if_counted_string_lh) 结构的类型定义。 该扩展必须确定此结构的 **length** 成员值中的字符串长度。

**注意**   如果字符串以 null 结尾，则**长度**成员不能包含终止 null 字符。

 

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 开关参数的 OID 查询请求 \_ \_ ，并返回以下状态代码之一。

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
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>信息缓冲区的长度太小，无法返回 OID 查询请求的 OID_SWITCH_PARAMETERS 结构。 可扩展交换机的基础微型端口边缘设置 <strong>数据。QUERY_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
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
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

