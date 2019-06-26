---
title: MdlAfterReqCompletedWriteA 规则 (kmdf)
description: MdlAfterReqCompletedWriteA 规则指定，EvtIoWrite 回调函数内检索到的内存描述符列表 (MDL) 对象后，无法访问已完成的 I/O 请求。
ms.assetid: 325a5ef6-459d-4457-bbad-774c76ddcdb9
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedWriteA 规则 (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedWriteA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fba67ff2efd6109296e074ad1d1a988444bea783
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393053"
---
# <a name="mdlafterreqcompletedwritea-rule-kmdf"></a>MdlAfterReqCompletedWriteA 规则 (kmdf)


**MdlAfterReqCompletedWriteA**规则指定内[ *EvtIoWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)回调函数不能为检索到的内存描述符列表 (MDL) 对象I/O 请求完成后，访问。

中的驱动程序*EvtIoWrite*设备的 I/O 队列，请通过调用检索到的请求缓冲区的回调函数[ **WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)方法不能访问之后调用[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)， [ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)，或[ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) I/O 请求。

此规则会考虑以下 MDL 访问函数：

[**WDF\_内存\_描述符\_INIT\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl)
[**MmGetMdlByteCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount) 
[ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl) （第一个和第二个参数） [ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers) 
 [ **MmGetMdlPfnArray**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetMdlByteOffset** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [ **MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>MdlAfterReqCompletedWriteA</strong>规则。</p>
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

[**WDF\_内存\_描述符\_INIT\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl)
[**WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)
 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**WdfRequestCompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
 [ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
[**WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
 [ **IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl)
[**KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers) 
 [**MmGetMdlByteCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount)
[**MmGetMdlByteOffset** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [ **MmGetMdlPfnArray**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)








