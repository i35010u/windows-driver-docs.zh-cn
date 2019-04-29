---
title: MemAfterReqCompletedIoctl 规则 (kmdf)
description: MemAfterReqCompletedIoctl 规则指定，在 EvtIoDeviceControl 回调函数的内部 framework 内存对象后，无法访问已完成的 I/O 请求。
ms.assetid: c737fb04-f517-41dd-b5b9-474f1dfb7c36
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedIoctl 规则 (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedIoctl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca39a17a7a599b1eb7efbad3b2a9eb61cd82ee57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386396"
---
# <a name="memafterreqcompletedioctl-rule-kmdf"></a>MemAfterReqCompletedIoctl 规则 (kmdf)


**MemAfterReqCompletedIoctl**规则指定内[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)回调函数不能后我访问 framework 内存对象/O 请求完成。

中的驱动程序[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)回调函数，通过调用检索到的 framework 内存对象[ **WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)或[ **WdfRequestRetrieveOutputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550019)之后调用，不能访问方法[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)， [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)上的 I/O 请求。

此规则会考虑以下内存访问方法：

[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)
[**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MemAfterReqCompletedIoctl</strong>规则。</p>
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
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550015) 
 [ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)








