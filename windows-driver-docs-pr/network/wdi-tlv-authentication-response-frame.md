---
title: WDI_TLV_AUTHENTICATION_RESPONSE_FRAME
description: WDI_TLV_ASSOCIATION_RESPONSE_FRAME 是包含身份验证响应帧 TLV。
ms.assetid: 0BD8BDD9-7D51-413F-8740-FD49F71249B1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AUTHENTICATION_RESPONSE_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d17dd3a3f39809a57d874ebe009ed3f09bd76edb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526402"
---
# <a name="wditlvauthenticationresponseframe"></a>WDI\_TLV\_身份验证\_响应\_帧


WDI\_TLV\_关联\_响应\_帧是包含身份验证响应帧 TLV。

## <a name="tlv-type"></a>TLV 类型


0x124

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含了失败代码收到的身份验证响应。 这不包括 802.11 MAC 报头。 |

 

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

 

 




