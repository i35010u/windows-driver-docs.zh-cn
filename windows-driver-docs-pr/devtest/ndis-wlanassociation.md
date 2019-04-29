---
title: WlanAssociation 规则 (ndis)
description: WlanAssociation 规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 关联序列。
ms.assetid: 3F457C06-29F1-4730-92D5-5B98CD459FD1
ms.date: 05/21/2018
keywords:
- WlanAssociation 规则 (ndis)
topic_type:
- apiref
api_name:
- WlanAssociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7bd8cc9f8622f63aeaa0dc9ca807f15655234436
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352871"
---
# <a name="wlanassociation-rule-ndis"></a>WlanAssociation 规则 (ndis)


**WlanAssociation**规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 关联序列。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00093004) |

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
[NDIS\_状态\_DOT11\_关联\_开始](https://msdn.microsoft.com/library/windows/hardware/ff567321)
 

 





