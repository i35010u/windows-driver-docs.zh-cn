---
title: BufAfterReqCompletedIntIoctl 规则 (kmdf)
description: BufAfterReqCompletedIntIoctl 规则指定，在请求完成后，其缓冲区无法访问 （在仅 EvtIoInternalDeviceControl 回调函数）。
ms.assetid: 6632262F-8163-4B4C-9B07-BCBD7CDA6E33
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedIntIoctl 规则 (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedIntIoctl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 415c9fba991f6b732a177ef1ff5f2932330ff290
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547133"
---
# <a name="bufafterreqcompletedintioctl-rule-kmdf"></a>BufAfterReqCompletedIntIoctl 规则 (kmdf)


**BufAfterReqCompletedIntIoctl**规则指定的请求完成后，无法访问其缓冲区 (内[ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768)回调函数仅）。 通过调用检索缓冲区[ **WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018)或[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)或[ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)或[ **WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)。

内[ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768) I/O 队列事件回调函数，通过调用检索到的请求缓冲区[ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)， [ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)， [ **WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)，或[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)请求完成后，无法访问。 在请求完成通过调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或**WdfRequestComplete**， [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)。 考虑以下可能的缓冲区访问函数：**WdfRequestRetrieveOutputBuffer**， **WdfRequestRetrieveUnsafeUserOutputBuffer**， **WdfRequestRetrieveInputBuffer**和**WdfRequestRetrieveUnsafeUserInputBuffer**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>BufAfterReqCompletedIntIoctl</strong>规则。</p>
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

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014) 
 [ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)
[**WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022) 
 [**WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)
 

 





