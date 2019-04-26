---
title: WDI_TLV_FT_AUTH_RESPONSE
description: WDI_TLV_FT_AUTH_RESPONSE 是 TLV 包含快速转换身份验证响应的字节 blob。
ms.assetid: BF9B37B4-EC5D-46AA-B334-C1214310964B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_AUTH_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a34954f5b82815ef62adeaf8009061fee1cfbb5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329733"
---
# <a name="wditlvftauthresponse"></a>WDI\_TLV\_FT\_AUTH\_RESPONSE


WDI\_TLV\_FT\_身份验证\_响应是包含快速转换身份验证响应的字节 blob TLV。

## <a name="tlv-type"></a>TLV 类型


0x10E

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                     |
|-----------|-------------------------------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含快速转换身份验证响应的字节 blob。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




