---
title: WDI_TLV_DELETE_CIPHER_KEY_INFO
description: WDI_TLV_DELETE_CIPHER_KEY_INFO 是包含的信息可确定要删除具有 OID_WDI_SET_DELETE_CIPHER_KEYS 单一密码密钥 TLV。
ms.assetid: 5AD84E05-9A25-4FE8-BDF4-CCBA89D09A3F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DELETE_CIPHER_KEY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b7751553c78fc2869dc5f49af846d6a6b8d98c27
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353615"
---
# <a name="wditlvdeletecipherkeyinfo"></a>WDI\_TLV\_DELETE\_CIPHER\_KEY\_INFO


WDI\_TLV\_删除\_密码\_密钥\_信息是包含的信息可确定要删除，但单个密码密钥 TLV [OID\_WDI\_设置\_删除\_密码\_密钥](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-delete-cipher-keys)。

## <a name="tlv-type"></a>TLV 类型


0x53

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                |
|---------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_对等方\_MAC\_地址**](wdi-tlv-peer-mac-address.md)          |                                | X        | 指定对等的 MAC 地址。 在至少一个 WDI\_TLV\_对等方\_MAC\_地址或 WDI\_TLV\_密码\_密钥\_ID 必须存在。 |
| [**WDI\_TLV\_CIPHER\_KEY\_ID**](wdi-tlv-cipher-key-id.md)                |                                | X        | 指定密码密钥 id。 在至少一个 WDI\_TLV\_对等方\_MAC\_地址或 WDI\_TLV\_密码\_密钥\_ID 必须存在。    |
| [**WDI\_TLV\_CIPHER\_KEY\_TYPE\_INFO**](wdi-tlv-cipher-key-type-info.md) |                                |          | 指定的密码密钥类型信息。                                                                                 |

 

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

 

 




