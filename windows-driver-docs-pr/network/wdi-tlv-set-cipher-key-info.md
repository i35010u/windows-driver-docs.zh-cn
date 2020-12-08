---
title: WDI_TLV_SET_CIPHER_KEY_INFO
description: WDI_TLV_SET_CIPHER_KEY_INFO 是一种 TLV，其中包含 OID_WDI_SET_ADD_CIPHER_KEYS 的密码密钥映射关键信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_CIPHER_KEY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 87a39d6ebbaf7be52bbff52c65037c7540c26cfd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834171"
---
# <a name="wdi_tlv_set_cipher_key_info"></a>WDI \_ TLV \_ 设置 \_ 密码 \_ 密钥 \_ 信息


WDI \_ tlv \_ 设置 \_ 密码 \_ 密钥 \_ 信息是一个 TLV，其中包含 OID 的密码密钥映射关键信息 [ \_ WDI \_ 设置 \_ 添加 \_ 密码 \_ 密钥](./oid-wdi-set-add-cipher-keys.md)。

## <a name="tlv-type"></a>TLV 类型


0x52

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 对等 \_ MAC \_ 地址**](wdi-tlv-peer-mac-address.md)                                     |                                | X        | 指定与此密钥关联的对等节点的 MAC 地址。 如果不存在，则假定这是默认键。 至少必须存在一个对等 MAC 地址或密码密钥 ID。 当键类型设置为 WDI \_ 密码 \_ 键类型成对键时，必须存在此字段 \_ \_ \_ ，并且当键类型设置为 WDI \_ 密码 \_ 键 \_ 类型 \_ 组 \_ 键时，可以存在此字段。 |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ ID**](wdi-tlv-cipher-key-id.md)                                           |                                | X        | 指定此密码密钥的 ID。 至少必须存在一个对等 MAC 地址或密码密钥 ID。 对于成对键，此字段不是必需的。                                                                                                                                                                                                            |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ 类型 \_ 信息**](wdi-tlv-cipher-key-type-info.md)                            |                                |          | 指定密码密钥类型信息。                                                                                                                                                                                                                                                                                                                        |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ 接收 \_ 序列 \_ 计数**](wdi-tlv-cipher-key-receive-sequence-count.md) |                                | X        | 指定 (PN) 的数据包编号的初始48位值，用于重放保护。 如果密码算法为 WDI \_ 密码 \_ 算法 \_ WEP40、WDI \_ 密码 \_ 算法 \_ WEP104 或 WDI \_ 密码 \_ 算法 \_ WEP，则这是可选的。                                                                                                                                        |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ CCMP 报头 \_ 密钥**](wdi-tlv-cipher-key-ccmp-key.md)                              |                                | X        | 指定 CCMP 报头密码算法密钥数据。 仅当密码算法为 WDI \_ cipher 算法 ccmp 报头时，才会出现这种情况 \_ \_ 。                                                                                                                                                                                                                                            |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ TKIP \_ 信息**](wdi-tlv-cipher-key-tkip-info.md)                            |                                | X        | 指定 TKIP 信息。 仅当密码算法为 WDI \_ cipher 算法 TKIP 时才会出现这种情况 \_ \_ 。                                                                                                                                                                                                                                                          |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ BIP \_ 密钥**](wdi-tlv-cipher-key-bip-key.md)                                |                                | X        | 指定 BIP 键。 仅当密码算法为 WDI \_ cipher 算法 BIP 时，才会出现这种情况 \_ \_ 。                                                                                                                                                                                                                                                                    |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ WEP \_ 密钥**](wdi-tlv-cipher-key-wep-key.md)                                |                                | X        | 指定 WEP 密钥。 仅当密码算法为 WDI \_ cipher \_ 算法 \_ WEP40、WDI \_ 密码 \_ 算法 \_ WEP104 或 WDI \_ 密码 \_ 算法 \_ WEP 时才会出现这种情况。                                                                                                                                                                                                            |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ IHV \_ 密钥**](wdi-tlv-cipher-key-ihv-key.md)                                |                                | X        | 指定 IHV 密码密钥。 仅当 [**WDI \_ TLV \_ 密码 \_ 密钥 \_ 类型 \_ 信息**](wdi-tlv-cipher-key-type-info.md) 在 WDI \_ cipher \_ 算法 \_ ihv \_ 开始到 WDI \_ 密码 \_ 算法 \_ ihv \_ 结束范围内时才会出现这种情况。                                                                                                                                                     |

 

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

 

