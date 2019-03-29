---
title: WDI_TLV_CIPHER_KEY_CCMP_KEY
description: WDI_TLV_CIPHER_KEY_CCMP_KEY 是 TLV 包含 OID_WDI_SET_ADD_CIPHER_KEY CCMP 密码算法的密钥数据。
ms.assetid: A4754EAC-AA54-45CC-A7C5-B78A2757E012
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_CCMP_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ae078e2089abc9c274fd4e39df036b5de07f7740
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568261"
---
# <a name="wditlvcipherkeyccmpkey"></a>WDI\_TLV\_CIPHER\_KEY\_CCMP\_KEY


WDI\_TLV\_密码\_密钥\_CCMP\_键是包含 CCMP 密码算法密钥数据的 TLV [OID\_WDI\_设置\_添加\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925855)。

## <a name="tlv-type"></a>TLV 类型


0x50

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                               |
|-----------|-------------------------------------------|
| UINT8\[\] | 指定 CCMP 密码算法的密钥数据。 |

 

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

 

 




