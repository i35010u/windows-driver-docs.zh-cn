---
title: BufAfterReqCompletedWriteA 规则 (kmdf)
description: BufAfterReqCompletedWriteA 规则指定，EvtIoWrite 回调函数中检索到的 I/O 请求缓冲区后，无法访问 I/O 请求完成。
ms.assetid: 4b7cd08f-8280-4bb6-be00-955ad8d2d015
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedWriteA 规则 (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedWriteA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af298bff645ba391188ebbb022d87a83cf28922e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540386"
---
# <a name="bufafterreqcompletedwritea-rule-kmdf"></a>BufAfterReqCompletedWriteA 规则 (kmdf)


BufAfterReqCompletedWriteA 规则指定，在[ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813) I/O 请求完成后，无法访问的回调函数，检索到的 I/O 请求缓冲区。

中的驱动程序**EvtIoWrite**回调函数，通过调用检索到的请求缓冲区

[**WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)或[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022)后调用，不能访问[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或者[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 请求。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>BufAfterReqCompletedWriteA</strong>规则。</p>
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

[**WDF\_内存\_描述符\_INIT\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552393)
[**WdfMemoryAssignBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548697)
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)
[**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 
[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)
 [ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
[**WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022) 
 [ **RtlCompareMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561778)
[**RtlMoveMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562030) 
 [ **RtlZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563610)
[**ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)
 

 





