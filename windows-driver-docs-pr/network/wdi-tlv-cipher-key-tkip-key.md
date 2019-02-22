---
title: WDI_TLV_CIPHER_KEY_TKIP_KEY
description: WDI_TLV_CIPHER_KEY_TKIP_KEY 是包含 TKIP 密钥材料 TLV。
ms.assetid: 73E4F051-5CC3-4F9E-9AFD-F33FAAC5A39D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TKIP_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 20b55f119ab3565dfec8b1b2a6373fba2069a549
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545646"
---
# <a name="wditlvcipherkeytkipkey"></a>WDI\_TLV\_密码\_密钥\_TKIP\_密钥


WDI\_TLV\_密码\_密钥\_TKIP\_键是包含 TKIP 密钥材料 TLV。

## <a name="tlv-type"></a>TLV 类型


0x49

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                      |
|-----------|------------------------------------------------------------------|
| UINT8\[\] | 指定 TKIP 密钥材料的 UINT8 元素数组。 |

 

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

 

 




