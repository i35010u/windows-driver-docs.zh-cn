---
title: RequestSendAndForgetNoFormatting 规则（kmdf）
description: RequestSendAndForgetNoFormatting 规则验证驱动程序在将请求发送到带有发送选项 WDF \_ 请求 \_ 发送选项 "发送 \_ \_ \_ 并 \_ 忘记" 的 i/o 目标之前，不会使用 i/o 目标格式设置函数对请求进行格式设置。
ms.assetid: C98C0C04-3345-49D6-9669-40D1A4F9CDBB
ms.date: 05/21/2018
keywords:
- RequestSendAndForgetNoFormatting 规则（kmdf）
topic_type:
- apiref
api_name:
- RequestSendAndForgetNoFormatting
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 232b77342926194130957d585531c38b7385e1ab
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916338"
---
# <a name="requestsendandforgetnoformatting-rule-kmdf"></a>RequestSendAndForgetNoFormatting 规则（kmdf）


**RequestSendAndForgetNoFormatting**规则验证驱动程序在将请求发送到带有发送选项 WDF \_ 请求 \_ 发送选项 "发送 \_ \_ \_ 并 \_ 忘记" 的 i/o 目标之前，不会使用 i/o 目标格式设置函数对请求进行格式设置。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>RequestSendAndForgetNoFormatting</strong>规则。</p>
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

[**WdfIoTargetFormatRequestForInternalIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl) 
[**WdfIoTargetFormatRequestForInternalIoctlOthers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers) 
[**WdfIoTargetFormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl) 
[**WdfIoTargetFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread) 
[**WdfIoTargetFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite) 
[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 
[**WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer) 
[**WdfUsbTargetDeviceFormatRequestForCyclePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport) 
[**WdfUsbTargetDeviceFormatRequestForString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforstring) 
[**WdfUsbTargetDeviceFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb) 
[**WdfUsbTargetPipeFormatRequestForAbort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort) 
[**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread) 
[**WdfUsbTargetPipeFormatRequestForReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset) 
[**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb) 
[**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)
 

 





