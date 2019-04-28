---
title: BufAfterReqCompletedIntIoctlA rule (kmdf)
description: BufAfterReqCompletedIntIoctlA 规则验证，在请求完成后，其缓冲区无法访问 （在内部 EvtIoInternalDeviceControl 回调）。
ms.assetid: 3635DB6D-00C7-44DD-B05A-7EAA16B18937
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedIntIoctlA rule (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedIntIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9ff7399898151f87927aef1fb3f2df372beed0b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340425"
---
# <a name="bufafterreqcompletedintioctla-rule-kmdf"></a>BufAfterReqCompletedIntIoctlA rule (kmdf)


**BufAfterReqCompletedIntIoctlA**规则验证的请求完成后，无法访问其缓冲区 (内[ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768)回调仅）。 通过调用检索到缓冲区[ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)或[ **WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018)或[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022)或[ **WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)。

内[ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768) I/O 队列事件回调函数，通过调用检索到的请求缓冲区[ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)或[ **WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018)或[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022)或[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)不能访问后[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)方法具有已在请求时调用。 考虑以下可能的缓冲区访问函数：[**RtlMoveMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562030) （使用作为第一个和第二个参数的缓冲区）， [ **RtlZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563610)， [ **RtlCompareMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561778)， [ **ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)， [ **ZwWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff567121)， [ **WDF\_内存\_描述符\_INIT\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552393)， [ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)， [ **WdfMemoryAssignBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548697)， [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)， [ **WdfMemoryCopyToBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548703)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>BufAfterReqCompletedIntIoctlA</strong>规则。</p>
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

[**WDF\_内存\_描述符\_INIT\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff552393)
[**WdfMemoryAssignBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548697)
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)
[**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 
[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)
 [ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
[**WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018) 
 [ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022) 
 [ **WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)
[**RtlCompareMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561778) 
 [**RtlMoveMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562030)
[**RtlZeroMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563610) 
 [ **ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)
 

 





