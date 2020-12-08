---
title: WDI_TLV_CIPHER_KEY_TKIP_MIC
description: WDI_TLV_CIPHER_KEY_TKIP_MIC 是包含 TKIP MIC 材料的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TKIP_MIC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5215eb10d17b2730d219a32eb28a0b90d55bcff6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807981"
---
# <a name="wdi_tlv_cipher_key_tkip_mic"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ TKIP \_ MIC


WDI \_ tlv \_ 密码 \_ 密钥 \_ TKIP \_ mic 是包含 TKIP mic 材料的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x4A

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                      |
|-----------|------------------------------------------------------------------|
| UINT8\[\] | 指定 TKIP MIC 材料的 UINT8 元素的数组。 |

 

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

 

 




