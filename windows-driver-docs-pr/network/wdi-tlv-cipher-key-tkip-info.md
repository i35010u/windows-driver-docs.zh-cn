---
title: WDI_TLV_CIPHER_KEY_TKIP_INFO
description: WDI_TLV_CIPHER_KEY_TKIP_INFO 是包含 TKIP 信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TKIP_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b688fc71250b59eac5f462436987bf29eddb528f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837637"
---
# <a name="wdi_tlv_cipher_key_tkip_info"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ TKIP \_ 信息


WDI \_ tlv \_ 密码 \_ 密钥 \_ TKIP \_ 信息是包含 TKIP 信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x4B

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                    | 允许多个 TLV 实例 | 可选 | 说明                      |
|-------------------------------------------------------------------------|--------------------------------|----------|----------------------------------|
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ TKIP \_ 密钥**](wdi-tlv-cipher-key-tkip-key.md) |                                |          | 指定 TKIP 密钥材料。 |
| [**WDI \_ TLV \_ 密码 \_ 密钥 \_ TKIP \_ MIC**](wdi-tlv-cipher-key-tkip-mic.md) |                                |          | 指定 TKIP MIC 材料。 |

 

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

 

 




