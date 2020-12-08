---
title: WDI_TLV_CIPHER_KEY_IHV_KEY
description: WDI_TLV_CIPHER_KEY_IHV_KEY 是包含 IHV 密钥的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_IHV_KEY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e3f7c831eff811527ae7e9d876a436263007941f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824955"
---
# <a name="wdi_tlv_cipher_key_ihv_key"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ IHV \_ 密钥


WDI \_ tlv \_ 密码 \_ 密钥 \_ IHV \_ 密钥是包含 IHV 密钥的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x118

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                            |
|-----------|--------------------------------------------------------|
| UINT8\[\] | 指定 IHV 密钥的 UINT8 元素的数组。 |

 

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

 

 




