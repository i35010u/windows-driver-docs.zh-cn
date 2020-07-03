---
title: MemAfterReqCompletedWriteA 规则（kmdf）
description: MemAfterReqCompletedWriteA 规则指定在 EvtIoWrite 回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。
ms.assetid: ac1d8aa5-9b33-4118-8f9a-11673d0f827c
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedWriteA 规则（kmdf）
topic_type:
- apiref
api_name:
- MemAfterReqCompletedWriteA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f682803499869aedb00ee77a401d46d63cfce585
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918151"
---
# <a name="memafterreqcompletedwritea-rule-kmdf"></a>MemAfterReqCompletedWriteA 规则（kmdf）


**MemAfterReqCompletedWriteA**规则指定在[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。

在驱动程序的[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)回调函数中，无法在对 i/o 请求调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)或[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)后访问通过调用[**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)方法检索到的 framework 内存对象。

此规则考虑以下八种访问方法：

[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 
[**WDF \_内存 \_ 说明符 \_ INIT \_ HANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle) 
 [**WdfMemoryAssignBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer) 
 [**WdfMemoryCopyToBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [**WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 
 [**WdfObjectReference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference) 
 [**WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference) 
 [**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>MemAfterReqCompletedWriteA</strong>规则。</p>
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

[**WDF \_内存 \_ 说明符 \_ INIT \_ HANDLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle) 
 [**WdfMemoryAssignBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer) 
 [**WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 
 [**WdfMemoryCopyToBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 
 [**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 
 [**WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference) 
 [**WdfObjectReference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference) 
 [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
 [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)








