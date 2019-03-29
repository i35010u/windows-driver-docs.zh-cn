---
title: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS
description: WDI_TLV_LINK_STATE_CHANGE_PARAMETERS 是包含链接状态 TLV NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 更改的参数。
ms.assetid: 808C2E69-B713-41A3-AFB9-7441D2A96867
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LINK_STATE_CHANGE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f343df41fe54f377d58831b797273936808771fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577128"
---
# <a name="wditlvlinkstatechangeparameters"></a>WDI\_TLV\_链接\_状态\_更改\_参数


WDI\_TLV\_链接\_状态\_更改\_参数是包含链接状态更改参数 TLV [NDIS\_状态\_WDI\_指示\_链接\_状态\_更改](https://msdn.microsoft.com/library/windows/hardware/dn925638)。

## <a name="tlv-type"></a>TLV 类型


0x56

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/dn926071) | 指定远程对等方的 MAC 地址。                                                                                                                                   |
| UINT32                                            | 指定当前 TX 链接速度。 这是为此虚拟化的端口的当前 TX 链接速度的值，以千比特 / 秒。 转换是 1 kbps = 1000 bps。 |
| UINT32                                            | 指定当前 RX 链接速度。 这是为此虚拟化的端口的当前 RX 链接速度的值，以千比特 / 秒。 转换是 1 kbps = 1000 bps。 |
| UINT8                                             | 指定当前链接质量。 这是一个介于 0 和 100 之间的值，是此虚拟化的端口的当前链接质量。                                               |

 

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

 

 




