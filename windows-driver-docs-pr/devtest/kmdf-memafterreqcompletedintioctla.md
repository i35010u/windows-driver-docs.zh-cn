---
title: MemAfterReqCompletedIntIoctlA 规则（kmdf）
description: MemAfterReqCompletedIntIoctlA 规则指定在 EvtIoInternalDeviceControl 回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。
ms.assetid: ff64d344-8b8e-4dec-adc3-d1e99f737e8a
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedIntIoctlA 规则（kmdf）
topic_type:
- apiref
api_name:
- MemAfterReqCompletedIntIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bca25bcb9c9186d6b723568793f38635ccf15bff
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918163"
---
# <a name="memafterreqcompletedintioctla-rule-kmdf"></a>MemAfterReqCompletedIntIoctlA 规则（kmdf）


**MemAfterReqCompletedIntIoctlA**规则指定在[*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。

[**在驱动**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)程序的*EvtIoInternalDeviceControl*回调函数中[**，调用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)WdfRequestRetrieveInputMemory 或 WdfRequestRetrieveOutputMemory 方法时，无法访问通过调用[**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)或[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)方法检索的 framework 内存对象[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)。

此规则考虑以下内存访问方法：

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>MemAfterReqCompletedIntIoctlA</strong>规则。</p>
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

[**WDF \_内存 \_ 描述符 \_ 初始化 \_ 处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle) 
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
 [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory) WdfRequestRetrieveOutputMemory








