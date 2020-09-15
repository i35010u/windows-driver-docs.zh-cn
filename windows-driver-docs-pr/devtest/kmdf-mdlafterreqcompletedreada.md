---
title: 'MdlAfterReqCompletedReadA 规则 (kmdf) '
description: MdlAfterReqCompletedReadA 规则指定在 EvtIoRead 回调函数中， (MDL) 对象的内存描述符列表无法在 i/o 请求完成后访问。
ms.assetid: 3e7c40a0-882e-45eb-8cf1-bee1096379ad
ms.date: 05/21/2018
keywords:
- 'MdlAfterReqCompletedReadA 规则 (kmdf) '
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedReadA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fbd8daee945d2bdeb8a8b0d2449c7e2a76311e01
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102256"
---
# <a name="mdlafterreqcompletedreada-rule-kmdf"></a>MdlAfterReqCompletedReadA 规则 (kmdf) 


**MdlAfterReqCompletedReadA**规则指定在[*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)回调函数中， (MDL) 对象的内存描述符列表无法在 i/o 请求完成后访问。

在驱动程序的*EvtIoRead*回调函数中，无法在对 i/o 请求调用[**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)或[**WdfRequestCompleteWithPriorityBoost**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)后访问通过调用[**WdfRequestRetrieveOutputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)方法检索到的请求缓冲区。

此规则考虑以下功能：

[**WDF \_内存 \_ 描述符 \_ 初始化 \_ MDL**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl) 
 [**MmGetMdlByteCount**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount) 
 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) 
 [**MmGetMdlVirtualAddress**](../kernel/mm-bad-pointer.md) 
 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) (第一个和第二个参数) [**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 
 [**MmGetMdlPfnArray**](../kernel/mm-bad-pointer.md) 
 [**MmGetMdlByteOffset**](../kernel/mm-bad-pointer.md) 
 [**MmPrepareMdlForReuse**](../kernel/mm-bad-pointer.md) 
 [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) WdfDmaTransactionInitialize

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>MdlAfterReqCompletedReadA</strong> 规则。</p>
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

[**WDF \_内存 \_ 描述符 \_ 初始化 \_ MDL**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl) 
 [**WdfDmaTransactionInitialize**](/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 
 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
 [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [**WdfRequestCompleteWithPriorityBoost**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
 [**WdfRequestRetrieveOutputWdmMdl**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) 
 [**IoBuildPartialMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) 
 [**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 
 [**MmGetMdlByteCount**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount) 
 [**MmGetMdlByteOffset**](../kernel/mm-bad-pointer.md) 
 [**MmGetMdlPfnArray**](../kernel/mm-bad-pointer.md) 
 [**MmGetMdlVirtualAddress**](../kernel/mm-bad-pointer.md) 
 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md) 
 [**MmPrepareMdlForReuse**](../kernel/mm-bad-pointer.md) MmPrepareMdlForReuse