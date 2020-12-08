---
title: WDI_TLV_CIPHER_KEY_CCMP_KEY
description: WDI_TLV_CIPHER_KEY_CCMP_KEY 是一种 TLV，其中包含 OID_WDI_SET_ADD_CIPHER_KEY 的 CCMP 报头密码算法密钥数据。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_CCMP_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4e71ba9b5953ea4fbc1e9ae4af54c84aab2651cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837643"
---
# <a name="wdi_tlv_cipher_key_ccmp_key"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ CCMP 报头 \_ 密钥


WDI \_ tlv \_ 密码 \_ 密钥 \_ CCMP 报头 \_ 密钥是一个 TLV，其中包含 OID 的 ccmp 报头密码算法 [密钥 \_ \_ \_ \_ \_ ](./oid-wdi-set-add-cipher-keys.md)数据。

## <a name="tlv-type"></a>TLV 类型


0x50

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                               |
|-----------|-------------------------------------------|
| UINT8\[\] | 指定 CCMP 报头密码算法密钥数据。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

