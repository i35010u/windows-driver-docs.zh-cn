---
title: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS 为 TLV，其中包含 OID_WDI_TASK_SEND_AP_ASSOCIATION_RESPONSE 的关联响应参数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bcf5557b86de6a0491940f706a97e0d2596fc957
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832099"
---
# <a name="wdi_tlv_association_response_parameters"></a>WDI \_ TLV \_ 关联 \_ 响应 \_ 参数


WDI \_ tlv \_ 关联 \_ 响应 \_ 参数是一个 Tlv，其中包含 [OID \_ WDI \_ TASK \_ 发送 \_ AP \_ 关联 \_ 响应](./oid-wdi-task-send-ap-association-response.md)的关联响应参数。

## <a name="tlv-type"></a>TLV 类型


0x97

## <a name="length"></a>长度


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
<th>描述</th>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

