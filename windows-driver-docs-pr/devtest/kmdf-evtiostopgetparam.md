---
title: EvtIoStopGetParam 规则 (kmdf)
description: EvtIoStopGetParam 规则检查 WdfRequestGetParameters EvtIoStop 回调不会调用。
ms.assetid: 4693DA4D-2298-45C3-8F07-24C861DD85BB
ms.date: 05/21/2018
keywords:
- EvtIoStopGetParam 规则 (kmdf)
topic_type:
- apiref
api_name:
- EvtIoStopGetParam
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ced0439dd1efb37d5dde920e09f793b789c4dec4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350422"
---
# <a name="evtiostopgetparam-rule-kmdf"></a>EvtIoStopGetParam 规则 (kmdf)


**EvtIoStopGetParam**规则检查[ **WdfRequestGetParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff549969)不会调用内[ *EvtIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541788)回调。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>EvtIoStopGetParam</strong>规则。</p>
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

[**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)
 

 





