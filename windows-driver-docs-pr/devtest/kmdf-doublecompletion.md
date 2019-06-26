---
title: DoubleCompletion 规则 (kmdf)
description: DoubleCompletion 规则指定，驱动程序必须完成的 I/O 请求两次。
ms.assetid: F005501B-29B5-42CE-8CAD-EDA00E1E5D82
ms.date: 05/21/2018
keywords:
- DoubleCompletion 规则 (kmdf)
topic_type:
- apiref
api_name:
- DoubleCompletion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 93e53ac8d7a49626a300ea14cc875fd22fc4f89d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394057"
---
# <a name="doublecompletion-rule-kmdf"></a>DoubleCompletion 规则 (kmdf)


**DoubleCompletion**规则指定，驱动程序必须完成的 I/O 请求两次。 不应在同一请求的行中两次调用以下方法：[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)， [ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)， [ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost).

此规则之间的差异并[DoubleCompletionLocal](kmdf-doublecompletionlocal.md)规则是 DoubleCompletionLocal 规则只执行默认 I/O 队列回调函数中。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>DoubleCompletion</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)
[**WdfIoQueueRetrieveNextRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievenextrequest) 
 [ **WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)
[**WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
 [ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
 

 





