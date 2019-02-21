---
title: StorPortNotification2 规则 (storport)
description: 此规则验证对 StorPortNotification 调用使用仅允许 （即记录） 的通知类型。
ms.assetid: 74363E6D-1D1B-484D-A558-8996DFE02FA8
ms.date: 05/21/2018
keywords:
- StorPortNotification2 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortNotification2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8fe18cc17e54e964de8c44f5e4504b8da695e28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554541"
---
# <a name="storportnotification2-rule-storport"></a>StorPortNotification2 规则 (storport)


此规则验证的调用**StorPortNotification**只允许使用 （即记录） 的通知类型。

允许的通知类型包括：

**BufferOverrunDetected**
**BusChangeDetected**
**LinkDown**
**LinkUp** 
**QueryTickCount**
**RequestComplete**
**RequestTimerCall** 
 **ResetDetected**
**WMIEvent**
**WMIReregister**

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>StorPortNotification2</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**StorPortNotification**](https://msdn.microsoft.com/library/windows/hardware/ff567433)








