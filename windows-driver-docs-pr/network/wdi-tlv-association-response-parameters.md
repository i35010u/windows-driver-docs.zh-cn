---
title: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS 为 TLV，其中包含 OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 的关联响应参数。
ms.assetid: FB116762-2064-48FA-B630-D5AE54657D10
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e94842d79f0fad1a9ebb8e5e423f2cbbdc209e25
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206177"
---
# <a name="wdi_tlv_association_response_parameters"></a>WDI \_ TLV \_ 关联 \_ 响应 \_ 参数


WDI \_ tlv \_ 关联 \_ 响应 \_ 参数是一个 Tlv，其中包含 [OID \_ WDI \_ TASK \_ 发送 \_ AP \_ 关联 \_ 响应](./oid-wdi-task-send-ap-association-response.md)的关联响应参数。

## <a name="tlv-type"></a>TLV 类型


0x97

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>指定是否接受关联请求。
<p>有效值为 0 (不接受) ，1 (接受) 。</p></td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>指定原因代码。 如果 accept request 设置为0，则此字段将提供一个将原因代码发送回对等适配器。</td>
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
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

