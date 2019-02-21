---
title: WDI_TLV_PMKID
description: WDI_TLV_PMKID 是包含 PMKID 值 TLV。
ms.assetid: 6873928B-7843-434F-AB80-6A7895D751A4
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PMKID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f5f1ed0f4fe17721a91fa3dbd12ea27ae6863b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540537"
---
# <a name="wditlvpmkid"></a>WDI\_TLV\_PMKID


WDI\_TLV\_PMKID 是包含 PMKID 值 TLV。

## <a name="tlv-type"></a>TLV 类型


0x9F

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述            |
|-----------|------------------------|
| UINT8\[\] | 一个 16 字节的 PMKID 值。 |

 

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

 

 




