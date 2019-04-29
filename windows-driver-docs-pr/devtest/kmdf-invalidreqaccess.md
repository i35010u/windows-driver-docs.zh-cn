---
title: InvalidReqAccess 规则 (kmdf)
description: InvalidReqAccess 规则指定后完成或取消不访问请求。
ms.assetid: dc7609a5-8b18-44b9-88b0-a9616bc220d4
ms.date: 05/21/2018
keywords:
- InvalidReqAccess 规则 (kmdf)
topic_type:
- apiref
api_name:
- InvalidReqAccess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9dbdfcad92d21b604f2ff0e2f252965c679f241c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356425"
---
# <a name="invalidreqaccess-rule-kmdf"></a>InvalidReqAccess 规则 (kmdf)


**InvalidReqAccess**规则指定后完成或取消不访问请求。 此规则与其他规则，例如，检查 double 完成状态的规则可能会重叠或检查请求的规则已标记为可取消两次。

请求将被视为无效，如果它已完成，标记为可取消，或取消后已发送。 该请求将被视为无效后，该请求不能传递给 **WdfRequest * * * Xxx*函数，当驱动程序调用除外**WdfRequestUnmarkCancelable**如果先前标记请求可取消。

此规则是类似于[ **InvalidReqAccessLocal** ](kmdf-invalidreqaccesslocal.md)规则; 但是， **InvalidReqAccessLocal**中默认 I/O 队列回调仅执行规则函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>InvalidReqAccess</strong>规则。</p>
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

[**WdfRequestAllocateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff549938)  
[**WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)  
[**WdfRequestChangeTarget**](https://msdn.microsoft.com/library/windows/hardware/ff549943)  
[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)  
[**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)  
[**WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)  
[**WdfRequestFormatRequestUsingCurrentType**](https://msdn.microsoft.com/library/windows/hardware/ff549955)  
[**WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)  
[**WdfRequestGetCompletionParams**](https://msdn.microsoft.com/library/windows/hardware/ff549961)  
[**WdfRequestGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff549963)  
[**WdfRequestGetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549965)  
[**WdfRequestGetIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549968)  
[**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)  
[**WdfRequestGetRequestorMode**](https://msdn.microsoft.com/library/windows/hardware/ff549971)  
[**WdfRequestIsFrom32BitProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549978)  
[**WdfRequestMarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff549983)  
[**WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)  
[**WdfRequestProbeAndLockUserBufferForRead**](https://msdn.microsoft.com/library/windows/hardware/ff549987)  
[**WdfRequestProbeAndLockUserBufferForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff549989)  
[**WdfRequestRequeue**](https://msdn.microsoft.com/library/windows/hardware/ff550012)  
[**WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)  
[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)  
[**WdfRequestRetrieveInputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550016)  
[**WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)  
[**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)  
[**WdfRequestRetrieveOutputWdmMdl**](https://msdn.microsoft.com/library/windows/hardware/ff550021)  
[**WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)  
[**WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)  
[**WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026)  
[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)  
[**WdfRequestSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff550030)  
[**WdfRequestSetInformation**](https://msdn.microsoft.com/library/windows/hardware/ff550032)  
[**WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)  
[**WdfRequestWdmFormatUsingStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550036)  
[**WdfRequestWdmGetIrp**](https://msdn.microsoft.com/library/windows/hardware/ff550037)  
 

 





