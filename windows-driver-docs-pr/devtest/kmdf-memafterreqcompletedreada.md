---
title: MemAfterReqCompletedReadA rule (kmdf)
description: MemAfterReqCompletedReadA 规则指定，在 EvtIoRead 回调函数的内部 framework 内存对象后，无法访问已完成的 I/O 请求。
ms.assetid: 5853fae3-3049-43d8-8452-a1afb268004b
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedReadA rule (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedReadA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b73b861ee7953b98c3d4d2f3e46d65b592f799bb
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393015"
---
# <a name="memafterreqcompletedreada-rule-kmdf"></a>MemAfterReqCompletedReadA rule (kmdf)


**MemAfterReqCompletedReadA**规则指定内[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)回调函数的 framework 内存对象无法访问后，I/O 请求已完成。

中的驱动程序*EvtIoRead*回调函数，通过调用检索到的 framework 内存对象[ **WdfRequestRetrieveOutputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)方法不能调用后，访问[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)， [ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) I/O 请求。

此规则会考虑以下内存访问方法：

[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)
[**WDF\_内存\_描述符\_INIT\_处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle) 
[ **WdfMemoryAssignBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)
[**WdfMemoryCopyToBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [ **WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)
[**WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference) 
 [ **WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)
[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>MemAfterReqCompletedReadA</strong>规则。</p>
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

[**WDF\_内存\_描述符\_INIT\_处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle)
[**WdfMemoryAssignBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)
 [ **WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)
[**WdfMemoryCopyToBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [ **WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)
[**WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) 
 [ **WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)
[**WdfObjectReference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference) 
 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**WdfRequestCompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)








