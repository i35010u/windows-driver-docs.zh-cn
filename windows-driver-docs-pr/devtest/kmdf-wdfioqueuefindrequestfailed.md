---
title: WdfIoQueueFindRequestFailed 规则 (kmdf)
description: WdfIoQueueFindRequestFailed 规则指定 WdfIoQueueRetrieveFoundRequest 或 WdfObjectDereference 应只调用 WdfIoQueueFindRequestFailed 返回状态后\_成功。
ms.assetid: 9D211A0A-36CB-4083-B379-EE1C34A7B50F
ms.date: 05/21/2018
keywords:
- WdfIoQueueFindRequestFailed 规则 (kmdf)
topic_type:
- apiref
api_name:
- WdfIoQueueFindRequestFailed
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d99b65b4a57267152a87b7f9fc89906d27fbb7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354387"
---
# <a name="wdfioqueuefindrequestfailed-rule-kmdf"></a>WdfIoQueueFindRequestFailed 规则 (kmdf)


**WdfIoQueueFindRequestFailed**规则指定[ **WdfIoQueueRetrieveFoundRequest** ](kmdf-wdfioqueueretrievefoundrequest.md)或者[ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)只应调用之后**WdfIoQueueFindRequestFailed**将返回状态\_成功。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>WdfIoQueueFindRequestFailed</strong>规则。</p>
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

[**WdfIoQueueFindRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547415)
[**WdfIoQueueRetrieveFoundRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548456)
[**WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)
 

 





