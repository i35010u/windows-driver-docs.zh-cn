---
title: WDI_TLV_FT_AUTH_REQUEST
description: WDI_TLV_FT_AUTH_REQUEST 是 TLV 包含快速转换身份验证请求的字节 blob。
ms.assetid: 4107314E-3C0A-4610-A4FB-BCBDBD1A8E65
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_AUTH_REQUEST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 50c62d072426cc7d2701ec455648b1abb5163d1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543809"
---
# <a name="wditlvftauthrequest"></a>WDI\_TLV\_FT\_AUTH\_REQUEST


WDI\_TLV\_FT\_身份验证\_请求是 TLV 包含快速转换身份验证请求的字节 blob。

## <a name="tlv-type"></a>TLV 类型


0x119

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含快速转换身份验证请求的字节 blob。 |

 

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

 

 




