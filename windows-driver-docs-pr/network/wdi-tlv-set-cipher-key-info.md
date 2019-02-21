---
title: WDI_TLV_SET_CIPHER_KEY_INFO
description: WDI_TLV_SET_CIPHER_KEY_INFO 是包含密码密钥映射的密钥信息 OID_WDI_SET_ADD_CIPHER_KEYS TLV。
ms.assetid: 6352284A-73CD-4B15-A057-80D0C8518CD5
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_CIPHER_KEY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b589762b6c8f098e5e2ff2b5b264e97d4baa490c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524860"
---
# <a name="wditlvsetcipherkeyinfo"></a>WDI\_TLV\_SET\_CIPHER\_KEY\_INFO


WDI\_TLV\_设置\_密码\_密钥\_信息是包含密码的密钥映射键信息 TLV [OID\_WDI\_设置\_添加\_密码\_密钥](https://msdn.microsoft.com/library/windows/hardware/dn925855)。

## <a name="tlv-type"></a>TLV 类型


0x52

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_对等方\_MAC\_地址**](wdi-tlv-peer-mac-address.md)                                     |                                | X        | 指定此密钥与之关联的对等方的 MAC 地址。 如果不存在，则假设这是默认密钥。 在至少一个对等的 MAC 地址或密码密钥 ID 必须存在。 此字段必须的存在时的密钥类型设置为 WDI\_密码\_密钥\_类型\_PAIRWISE\_键，并且可能的存在时的密钥类型设置为 WDI\_密码\_密钥\_类型\_组\_密钥。 |
| [**WDI\_TLV\_CIPHER\_KEY\_ID**](wdi-tlv-cipher-key-id.md)                                           |                                | X        | 指定此加密密钥的 ID。 在至少一个对等的 MAC 地址或密码密钥 ID 必须存在。 此字段不需要的成对密钥。                                                                                                                                                                                                            |
| [**WDI\_TLV\_CIPHER\_KEY\_TYPE\_INFO**](wdi-tlv-cipher-key-type-info.md)                            |                                |          | 指定的密码密钥类型信息。                                                                                                                                                                                                                                                                                                                        |
| [**WDI\_TLV\_CIPHER\_KEY\_RECEIVE\_SEQUENCE\_COUNT**](wdi-tlv-cipher-key-receive-sequence-count.md) |                                | X        | 指定初始 48 位值的数据包数 (PN)，用于进行重播保护。 这是可选的密码算法是否 WDI\_密码\_ALGO\_WEP40、 WDI\_密码\_ALGO\_WEP104 或 WDI\_密码\_ALGO\_WEP。                                                                                                                                        |
| [**WDI\_TLV\_CIPHER\_KEY\_CCMP\_KEY**](wdi-tlv-cipher-key-ccmp-key.md)                              |                                | X        | 指定的密码算法的 CCMP 数据。 这只会出现，如果密码算法是 WDI\_密码\_ALGO\_CCMP。                                                                                                                                                                                                                                            |
| [**WDI\_TLV\_密码\_密钥\_TKIP\_信息**](wdi-tlv-cipher-key-tkip-info.md)                            |                                | X        | 指定 TKIP 信息。 这只会出现，如果密码算法是 WDI\_密码\_ALGO\_TKIP。                                                                                                                                                                                                                                                          |
| [**WDI\_TLV\_CIPHER\_KEY\_BIP\_KEY**](wdi-tlv-cipher-key-bip-key.md)                                |                                | X        | 指定 BIP 键。 这只会出现，如果密码算法是 WDI\_密码\_ALGO\_BIP。                                                                                                                                                                                                                                                                    |
| [**WDI\_TLV\_CIPHER\_KEY\_WEP\_KEY**](wdi-tlv-cipher-key-wep-key.md)                                |                                | X        | 指定的 WEP 密钥。 这只会出现，如果密码算法是 WDI\_密码\_ALGO\_WEP40、 WDI\_密码\_ALGO\_WEP104 或 WDI\_密码\_ALGO\_WEP。                                                                                                                                                                                                            |
| [**WDI\_TLV\_CIPHER\_KEY\_IHV\_KEY**](wdi-tlv-cipher-key-ihv-key.md)                                |                                | X        | 指定 IHV 密码密钥。 如果这是仅存在[ **WDI\_TLV\_密码\_密钥\_类型\_信息**](wdi-tlv-cipher-key-type-info.md)处于范围内 WDI\_密码\_ALGO\_IHV\_启动到 WDI\_密码\_ALGO\_IHV\_结束。                                                                                                                                                     |

 

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

 

 




