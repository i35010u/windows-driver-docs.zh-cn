---
title: MemAfterReqCompletedWriteA 规则 (kmdf)
description: MemAfterReqCompletedWriteA 规则指定，在 EvtIoWrite 回调函数的内部 framework 内存对象后，无法访问已完成的 I/O 请求。
ms.assetid: ac1d8aa5-9b33-4118-8f9a-11673d0f827c
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedWriteA 规则 (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedWriteA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4b8962832468ae34f8553a7278e9306e20f2f00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533436"
---
# <a name="memafterreqcompletedwritea-rule-kmdf"></a>MemAfterReqCompletedWriteA 规则 (kmdf)


**MemAfterReqCompletedWriteA**规则指定内[ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813)回调函数不能在 I/O 后访问 framework 内存对象在请求完成。

中的驱动程序[ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813)回调函数，通过调用检索到的 framework 内存对象[ **WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)方法不能访问之后调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 请求。

此规则会考虑以下八个访问方法：

[**WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)
[**WDF\_内存\_描述符\_INIT\_处理**](https://msdn.microsoft.com/library/windows/hardware/ff552395) 
[ **WdfMemoryAssignBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548697)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758) 
 [ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MemAfterReqCompletedWriteA</strong>规则。</p>
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

[**WDF\_内存\_描述符\_INIT\_处理**](https://msdn.microsoft.com/library/windows/hardware/ff552395)
[**WdfMemoryAssignBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548697)
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)
[**WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734) 
 [ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)
[**WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758) 
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)








