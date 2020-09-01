---
title: WDI_TLV_CIPHER_KEY_TYPE_INFO
description: WDI_TLV_CIPHER_KEY_TYPE_INFO 是包含 OID_WDI_SET_ADD_CIPHER_KEYS 和 OID_WDI_SET_DELETE_CIPHER_KEYS 的密码密钥类型信息的 TLV。
ms.assetid: 1168D53D-A837-4E3F-8E31-FB86CF866BA3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CIPHER_KEY_TYPE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 006ca5592ef0739812738be71de1d40a0e6863c9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208511"
---
# <a name="wdi_tlv_cipher_key_type_info"></a>WDI \_ TLV \_ 密码 \_ 密钥 \_ 类型 \_ 信息


WDI \_ tlv \_ 密码 \_ 密钥 \_ 类型 \_ 信息是一个 TLV，其中包含 OID 的密码密钥类型信息 [ \_ WDI \_ 设置 \_ 添加 \_ 密码 \_ 密钥](./oid-wdi-set-add-cipher-keys.md) 和 [oid \_ WDI \_ 设置 \_ 删除 \_ 密码 \_ 密钥](./oid-wdi-set-delete-cipher-keys.md)。

## <a name="tlv-type"></a>TLV 类型


0x4E

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                 | 说明                                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)          | 指定使用密钥的密码算法。                                                                                                                                                                                                                                               |
| [**WDI \_ 密码 \_ 键 \_ 方向**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_direction) | 指定密钥应仅用于传输、仅接收还是用于传输。                                                                                                                                                                                                              |
| UINT8                                                                | 指定端口是否应在漫游时删除密钥。 如果将此值设置为0，则当端口从 BSS 网络断开连接或连接到 BSS 网络时，必须删除该密钥。 如果此值设置为1，则应删除显式删除或重置请求上的键。 |
| [**WDI \_ 密码 \_ 键 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_key_type)           | 指定要发布的密钥的类型。                                                                                                                                                                                                                                                      |

 

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

 

