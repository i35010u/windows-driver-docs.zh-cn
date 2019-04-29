---
title: ReqCompletionRoutine 规则 (kmdf)
description: ReqCompletionRoutine 规则指定一个请求发送到的 I/O 目标之前，必须设置完成例程。
ms.assetid: 0ddf6980-0540-4224-9800-3cd534f03230
ms.date: 05/21/2018
keywords:
- ReqCompletionRoutine 规则 (kmdf)
topic_type:
- apiref
api_name:
- ReqCompletionRoutine
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4b4a897ad6a9b90cf1ee010372c6c928ceabd71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384106"
---
# <a name="reqcompletionroutine-rule-kmdf"></a>ReqCompletionRoutine 规则 (kmdf)


**ReqCompletionRoutine**规则指定一个请求发送到的 I/O 目标之前，必须设置完成例程。

如果请求不同步，发送或发送和忘了，不会发送 (通过指定**WDF\_请求\_发送\_选项\_发送\_AND\_忘记**标志)，该驱动程序应设置完成例程，以使 I/O 目标可以在请求完成时通知该驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ReqCompletionRoutine</strong>规则。</p>
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

[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfRequestSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff550030) See also
--------

[完成 I/O 请求](https://msdn.microsoft.com/library/windows/hardware/ff540740)
[同步取消和完成代码](https://msdn.microsoft.com/library/windows/hardware/ff544726)
[**WDF\_请求\_发送\_选项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff552493)
[**WDF\_请求\_发送\_选项**](https://msdn.microsoft.com/library/windows/hardware/ff552491)
 

 





