---
title: WDI_TLV_ACTION_FRAME_BODY
description: WDI_TLV_ACTION_FRAME_BODY 是包含操作帧的正文 TLV。
ms.assetid: 272782A9-F92E-4F32-A92B-B18EBE7C1803
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ACTION_FRAME_BODY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 561984937cf9fdda9f23d7368d4d25e744788a85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543623"
---
# <a name="wditlvactionframebody"></a>WDI\_TLV\_操作\_帧\_正文


WDI\_TLV\_操作\_帧\_正文是包含操作帧的正文 TLV。

## <a name="tlv-type"></a>TLV 类型


0xBE

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                           |
|-----------|-----------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含操作帧的正文。 |

 

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

 

 




