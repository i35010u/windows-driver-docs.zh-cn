---
title: WDI_TLV_CIPHER_KEY_ID
description: WDI_TLV_CIPHER_KEY_ID 是一个 TLV，其中包含 OID_WDI_SET_ADD_CIPHER_KEYS 和 OID_WDI_SET_DELETE_CIPHER_KEYS 的密码密钥 ID。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: da7ee5ebe41e8a423d777581ababb2605f086b1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837639"
---
# <a name="wdi_tlv_cipher_key_id"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ ID


WDI \_ tlv \_ 密码 \_ 密钥 \_ id 是一个 TLV，其中包含 OID 的密码密钥 id " [ \_ WDI" 设置 " \_ \_ 添加 \_ 密码 \_ 密钥](./oid-wdi-set-add-cipher-keys.md) " 和 " [oid \_ WDI \_ 集 \_ 删除 \_ 密码 \_ 密钥](./oid-wdi-set-delete-cipher-keys.md)"。

## <a name="tlv-type"></a>TLV 类型


0x4D

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                  |
|--------|------------------------------|
| UINT32 | 指定密码密钥 ID。 |

 

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

 

