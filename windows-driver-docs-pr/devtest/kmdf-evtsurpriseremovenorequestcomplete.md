---
title: EvtSurpriseRemoveNoRequestComplete 规则 (kmdf)
description: EvtSurpriseRemoveNoRequestComplete 规则指定 WDF 驱动程序不应完成从 EvtDeviceSurpriseRemoval 回调的请求，应改为使用自托管的 I/O 回调函数。
ms.assetid: A815CFA0-72A9-4FBC-8432-6212CB696F99
ms.date: 05/21/2018
keywords:
- EvtSurpriseRemoveNoRequestComplete 规则 (kmdf)
topic_type:
- apiref
api_name:
- EvtSurpriseRemoveNoRequestComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c90876debc6cd2beddd244e6373015d796b8ed2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350409"
---
# <a name="evtsurpriseremovenorequestcomplete-rule-kmdf"></a>EvtSurpriseRemoveNoRequestComplete 规则 (kmdf)


**EvtSurpriseRemoveNoRequestComplete**规则指定 WDF 驱动程序不应完成从请求[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)回调，而是应使用自托管的 I/O 回调函数。 *EvtDeviceSurpriseRemoval*回调不会同步与电源关闭路径。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>EvtSurpriseRemoveNoRequestComplete</strong>规则。</p>
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

<a name="applies-to"></a>适用对象
----------

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
 

 





