---
title: WDI_TLV_CIPHER_KEY_BIP_KEY
description: WDI_TLV_CIPHER_KEY_BIP_KEY 是 TLV 包含 OID_WDI_SET_ADD_CIPHER_KEYS BIP 密码算法的密钥数据。
ms.assetid: 99630BDF-9845-4E3D-AB18-5F5BAFCF7198
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_BIP_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3c7b2e3c0366cf95c85f5f17f33606c7a9167ce4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387190"
---
# <a name="wditlvcipherkeybipkey"></a>WDI\_TLV\_CIPHER\_KEY\_BIP\_KEY


WDI\_TLV\_密码\_密钥\_BIP\_键是包含 BIP 密码算法密钥数据的 TLV [OID\_WDI\_设置\_添加\_密码\_密钥](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-add-cipher-keys)。

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

 

 




