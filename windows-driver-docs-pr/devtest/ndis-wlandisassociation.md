---
title: WlanDisassociation 规则 (ndis)
description: WlanDisassociation 规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 解除关联序列。
ms.assetid: E9C115D5-8522-4275-B874-1DB673AE23F2
ms.date: 05/21/2018
keywords:
- WlanDisassociation 规则 (ndis)
topic_type:
- apiref
api_name:
- WlanDisassociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b217e6369b8dd06717cbed97dc0e7126a9bb6652
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352928"
---
# <a name="wlandisassociation-rule-ndis"></a>WlanDisassociation 规则 (ndis)


**WlanDisassociation**规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 解除关联序列。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00093006) |

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

 

<a name="applies-to"></a>适用对象
----------

[**MiniportHaltEx**](https://msdn.microsoft.com/library/windows/hardware/ff559388)
[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) 
 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)另请参阅
--------

[常规连接操作指南](https://msdn.microsoft.com/library/windows/hardware/ff552458)
[OID\_DOT11\_重置\_请求](https://msdn.microsoft.com/library/windows/hardware/ff569409)
[NDIS\_状态\_DOT11\_解除关联](https://msdn.microsoft.com/library/windows/hardware/ff567334)
[NDIS\_状态\_DOT11\_关联\_开始](https://msdn.microsoft.com/library/windows/hardware/ff567321)
 

 





