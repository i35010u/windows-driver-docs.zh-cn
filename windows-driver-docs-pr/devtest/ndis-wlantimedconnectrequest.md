---
title: WlanTimedConnectRequest 规则 (ndis)
description: WlanTimedConnectRequest 规则验证 OID\_DOT11\_CONNECT\_请求后跟 NDIS\_状态\_DOT11\_连接\_在 10 分钟内启动秒数。
ms.assetid: F40D92B1-CA48-4060-B9E2-A965900EAF7B
ms.date: 05/21/2018
keywords:
- WlanTimedConnectRequest 规则 (ndis)
topic_type:
- apiref
api_name:
- WlanTimedConnectRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a6be12d350032c24206ef0afc2dd4a1c4eb17da5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546477"
---
# <a name="wlantimedconnectrequest-rule-ndis"></a>WlanTimedConnectRequest 规则 (ndis)


**WlanTimedConnectRequest**规则验证 OID\_DOT11\_CONNECT\_请求后跟 NDIS\_状态\_DOT11\_连接\_在 10 秒内启动。

此外，NDIS\_状态\_DOT11\_连接\_开始指示仅当 OID\_DOT11\_CONNECT\_请求已完成并且 NDIS\_状态\_成功。 此规则仅适用于可扩展站端口 （端口 0）。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00094009) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MiniportHaltEx**](https://msdn.microsoft.com/library/windows/hardware/ff559388)
[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) 
 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)另请参阅
--------

[常规连接操作指南](https://msdn.microsoft.com/library/windows/hardware/ff552458)
 

 





