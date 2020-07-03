---
title: DoubleCompletion 规则（kmdf）
description: DoubleCompletion 规则指定驱动程序不得完成 i/o 请求两次。
ms.assetid: F005501B-29B5-42CE-8CAD-EDA00E1E5D82
ms.date: 05/21/2018
keywords:
- DoubleCompletion 规则（kmdf）
topic_type:
- apiref
api_name:
- DoubleCompletion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d974db4ef8576ff2bdffb3965f4044b0d1bda924
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916237"
---
# <a name="doublecompletion-rule-kmdf"></a>DoubleCompletion 规则（kmdf）


**DoubleCompletion**规则指定驱动程序不得完成 i/o 请求两次。 对于同一请求，不应在一行中调用以下方法两次： [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、 [**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)。

此规则与[DoubleCompletionLocal](kmdf-doublecompletionlocal.md)规则之间的区别在于仅在默认 i/o 队列回调函数内执行 DoubleCompletionLocal 规则。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>DoubleCompletion</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest) 
[**WdfIoQueueRetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest) 
[**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject) 
[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
 

 





