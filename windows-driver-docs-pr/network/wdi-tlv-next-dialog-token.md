---
title: WDI_TLV_NEXT_DIALOG_TOKEN
description: WDI_TLV_NEXT_DIALOG_TOKEN 是一个 TLV，其中包含要在下一个操作框中使用的对话框标记。
ms.assetid: B11331CB-50D3-4A3B-93A5-359ABD918E70
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NEXT_DIALOG_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 86609b015ad4fdc5507f923b284285a629f36142
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207771"
---
# <a name="wdi_tlv_next_dialog_token"></a>WDI \_ TLV \_ 下一个 \_ 对话框 \_ 令牌


WDI \_ tlv \_ 下一个 \_ 对话框 \_ 令牌是一个 tlv，其中包含要在下一个操作框架中使用的对话框令牌。

## <a name="tlv-type"></a>TLV 类型


0xE1

## <a name="length"></a>Length


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 说明                                           |
|-------|-------------------------------------------------------|
| UINT8 | 要在下一个操作框中使用的对话框标记。 |

 

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

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 获取 \_ 下一个 \_ 操作 \_ 框架 \_ 对话框 \_ 令牌](./oid-wdi-get-next-action-frame-dialog-token.md)

 

