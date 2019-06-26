---
title: OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN
description: OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN 请求 DialogToken 要在下一步操作框架中使用。
ms.assetid: EB5F6077-1566-41AE-B414-9ECF24BAE982
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_NEXT_ACTION_FRAME_DIALOG_TOKEN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fceb6564af7d2c38478f110bbcfa06182524adbe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353671"
---
# <a name="oidwdigetnextactionframedialogtoken"></a>OID\_WDI\_GET\_NEXT\_ACTION\_FRAME\_DIALOG\_TOKEN


OID\_WDI\_获取\_下一步\_操作\_帧\_对话框\_令牌请求 DialogToken 要在下一步操作框架中使用。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| Port  | 否                       | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


任何其他参数。 标头中的数据就足够了。
## <a name="get-property-results"></a>获取属性的结果


| TLV                                                                     | 允许多个 TLV 实例 | 可选 | 描述     |
|-------------------------------------------------------------------------|--------------------------------|----------|-----------------|
| [**WDI\_TLV\_NEXT\_DIALOG\_TOKEN**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-next-dialog-token) |                                |          | 对话框标志。 |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




