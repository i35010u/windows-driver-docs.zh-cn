---
title: WDI_TLV_CIPHER_KEY_BIP_KEY
description: WDI_TLV_CIPHER_KEY_BIP_KEY 是 TLV 包含 OID_WDI_SET_ADD_CIPHER_KEYS BIP 密码算法的密钥数据。
ms.assetid: 99630BDF-9845-4E3D-AB18-5F5BAFCF7198
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_BIP_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 405b4c40ba8ccd2ebc37f9e8a27dc1cf1a55d4c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567274"
---
# <a name="wditlvcipherkeybipkey"></a>WDI\_TLV\_CIPHER\_KEY\_BIP\_KEY


WDI\_TLV\_密码\_密钥\_BIP\_键是包含 BIP 密码算法密钥数据的 TLV [OID\_WDI\_设置\_添加\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925855)。

## <a name="tlv-type"></a>TLV 类型


0x51

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                              |
|-----------|------------------------------------------|
| UINT8\[\] | 指定 BIP 密码算法的密钥数据。 |

 

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

 

 




