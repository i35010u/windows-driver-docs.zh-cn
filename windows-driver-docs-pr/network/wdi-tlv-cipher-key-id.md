---
title: WDI_TLV_CIPHER_KEY_ID
description: WDI_TLV_CIPHER_KEY_ID 是包含一种密码 TLV OID_WDI_SET_ADD_CIPHER_KEYS 和 OID_WDI_SET_DELETE_CIPHER_KEYS 密钥 ID。
ms.assetid: 24076B2A-FAC2-4509-9F1C-7F2AF57883CF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a6abe0f2d217250b3b645a9a9d06ea38ffab2dde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554832"
---
# <a name="wditlvcipherkeyid"></a>WDI\_TLV\_CIPHER\_KEY\_ID


WDI\_TLV\_密码\_密钥\_ID 是包含一种密码 TLV 密钥的 ID [OID\_WDI\_设置\_添加\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925855)并[OID\_WDI\_设置\_删除\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925929)。

## <a name="tlv-type"></a>TLV 类型


0x4D

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                  |
|--------|------------------------------|
| UINT32 | 指定密码密钥 id。 |

 

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

 

 




