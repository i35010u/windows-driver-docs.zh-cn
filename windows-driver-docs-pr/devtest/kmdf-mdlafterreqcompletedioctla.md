---
title: MdlAfterReqCompletedIoctlA 规则（kmdf）
description: MdlAfterReqCompletedIoctlA 规则指定在 EvtIoDeviceControl 回调函数中，内存描述符列表（MDL）在 i/o 请求完成后无法访问。
ms.assetid: 694d3370-d739-4d6b-abc1-636eb90ea0b3
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedIoctlA 规则（kmdf）
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d55097fa41b0f38b14db8c39e44d3f032d4e258
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918175"
---
# <a name="mdlafterreqcompletedioctla-rule-kmdf"></a>MdlAfterReqCompletedIoctlA 规则（kmdf）


**MdlAfterReqCompletedIoctlA**规则指定在[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)回调函数中，内存描述符列表（MDL）在 i/o 请求完成后无法访问。

在驱动程序的[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)回调函数中，通过调用[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)或[**WDFREQUESTRETRIEVEOUTPUTWDMMDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)方法检索到的 MDL 在对 i/o 请求调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)或[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)后无法访问。

此规则查看以下两个 MDL 访问方法：

[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) 
[ **WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>MdlAfterReqCompletedIoctlA</strong>规则。</p>
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

[**WDF \_内存 \_ 描述符 \_ 初始化 \_ MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl) 
 [**WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 
 [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
 [**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) 
 [**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl) 
 [**IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) 
 [**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 
 [**MmGetMdlByteCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount) 
 [**MmGetMdlByteOffset**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**MmGetMdlPfnArray**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)








