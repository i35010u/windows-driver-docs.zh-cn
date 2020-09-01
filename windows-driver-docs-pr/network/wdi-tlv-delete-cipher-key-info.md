---
title: WDI_TLV_DELETE_CIPHER_KEY_INFO
description: WDI_TLV_DELETE_CIPHER_KEY_INFO 是一种 TLV，其中包含用于标识要在 OID_WDI_SET_DELETE_CIPHER_KEYS 中删除的单个密码密钥的信息。
ms.assetid: 5AD84E05-9A25-4FE8-BDF4-CCBA89D09A3F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DELETE_CIPHER_KEY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5cb504c6c1b39235112f3c8ea210b4ed46db4de9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214296"
---
# <a name="wdi_tlv_delete_cipher_key_info"></a>WDI \_ TLV \_ 删除 \_ 密码 \_ 密钥 \_ 信息


WDI \_ tlv \_ 删除 \_ 密码 \_ 密钥 \_ 信息是一个 TLV，其中包含用于标识要删除的单个密码密钥的信息，可使用 [OID \_ WDI \_ 设置 \_ 删除 \_ 密码 \_ 密钥](./oid-wdi-set-delete-cipher-keys.md)。

## <a name="tlv-type"></a>TLV 类型


0x53

## <a name="length"></a>Length


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                      | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                |
|---------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 对等 \_ MAC \_ 地址**](wdi-tlv-peer-mac-address.md)          |                                | X        | 指定对等 MAC 地址。 至少必须有一个 WDI \_ tlv \_ 对等 \_ MAC \_ 地址或 WDI \_ tlv \_ 密码 \_ 密钥 \_ ID。 |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ ID**](wdi-tlv-cipher-key-id.md)                |                                | X        | 指定密码密钥 ID。 至少必须有一个 WDI \_ tlv \_ 对等 \_ MAC \_ 地址或 WDI \_ tlv \_ 密码 \_ 密钥 \_ ID。    |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ 类型 \_ 信息**](wdi-tlv-cipher-key-type-info.md) |                                |          | 指定密码密钥类型信息。                                                                                 |

 

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

 

