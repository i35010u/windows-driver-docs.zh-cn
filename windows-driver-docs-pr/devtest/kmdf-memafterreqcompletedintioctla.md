---
title: 'MemAfterReqCompletedIntIoctlA 规则 (kmdf) '
description: MemAfterReqCompletedIntIoctlA 规则指定在 EvtIoInternalDeviceControl 回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。
ms.date: 05/21/2018
keywords:
- 'MemAfterReqCompletedIntIoctlA 规则 (kmdf) '
topic_type:
- apiref
api_name:
- MemAfterReqCompletedIntIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85b4fb53b0fe4a951ce2167452974c448bccd5cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790031"
---
# <a name="memafterreqcompletedintioctla-rule-kmdf"></a>MemAfterReqCompletedIntIoctlA 规则 (kmdf) 


**MemAfterReqCompletedIntIoctlA** 规则指定在 [*EvtIoInternalDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)回调函数中，在 i/o 请求完成后，不能访问 framework 内存对象。

[**在驱动**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)程序的 *EvtIoInternalDeviceControl* 回调函数中 [**，调用**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)WdfRequestRetrieveInputMemory 或 WdfRequestRetrieveOutputMemory 方法时，无法访问通过调用 [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)或 [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)方法检索的 framework 内存对象 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)。

此规则考虑以下内存访问方法：

[**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 
[**WDF \_内存 \_ 说明符 \_ INIT \_ HANDLE**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle) 
 [**WdfMemoryAssignBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer) 
 [**WdfMemoryCopyToBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [**WdfMemoryCopyFromBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 
 [**WdfObjectReference**](../wdf/wdfobjectreference.md) 
 [**WdfObjectDereference**](../wdf/wdfobjectdereference.md) 
 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>MemAfterReqCompletedIntIoctlA</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WDF \_内存 \_ 描述符 \_ 初始化 \_ 处理**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle) 
 [**WdfMemoryAssignBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer) 
 [**WdfMemoryCopyFromBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer) 
 [**WdfMemoryCopyToBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [**WdfMemoryGetBuffer**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer) 
 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 
 [**WdfObjectDereference**](../wdf/wdfobjectdereference.md) 
 [**WdfObjectReference**](../wdf/wdfobjectreference.md) 
 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [**WdfRequestCompleteWithPriorityBoost**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
 [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 
 [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory) WdfRequestRetrieveOutputMemory
