---
title: WDI_TLV_CIPHER_KEY_ID
description: WDI_TLV_CIPHER_KEY_ID 是一个 TLV，其中包含 OID_WDI_SET_ADD_CIPHER_KEYS 和 OID_WDI_SET_DELETE_CIPHER_KEYS 的密码密钥 ID。
ms.assetid: 24076B2A-FAC2-4509-9F1C-7F2AF57883CF
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: edfd3a86075635f2572f641120789d8f664065be
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212307"
---
# <a name="wdi_tlv_cipher_key_id"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ ID


WDI \_ tlv \_ 密码 \_ 密钥 \_ id 是一个 TLV，其中包含 OID 的密码密钥 id " [ \_ WDI" 设置 " \_ \_ 添加 \_ 密码 \_ 密钥](./oid-wdi-set-add-cipher-keys.md) " 和 " [oid \_ WDI \_ 集 \_ 删除 \_ 密码 \_ 密钥](./oid-wdi-set-delete-cipher-keys.md)"。

## <a name="tlv-type"></a>TLV 类型


0x4D

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                  |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

