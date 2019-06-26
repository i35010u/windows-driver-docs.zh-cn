---
title: WDI_TLV_NEXT_DIALOG_TOKEN
description: WDI_TLV_NEXT_DIALOG_TOKEN 是包含对话框标记以在下一步操作框架中使用 TLV。
ms.assetid: B11331CB-50D3-4A3B-93A5-359ABD918E70
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_NEXT_DIALOG_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 00eeab719c061efbeac7278d0c985d7bbd6c7427
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385718"
---
# <a name="wditlvnextdialogtoken"></a>WDI\_TLV\_NEXT\_DIALOG\_TOKEN


WDI\_TLV\_下一步\_对话框\_令牌是包含对话框标记以在下一步操作框架中使用 TLV。

## <a name="tlv-type"></a>TLV 类型


0xE1

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                           |
|-------|-------------------------------------------------------|
| UINT8 | 要在下一步操作框架中使用的对话框标记。 |

 

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

## <a name="see-also"></a>请参阅


[OID\_WDI\_GET\_NEXT\_ACTION\_FRAME\_DIALOG\_TOKEN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-next-action-frame-dialog-token)

 

 




