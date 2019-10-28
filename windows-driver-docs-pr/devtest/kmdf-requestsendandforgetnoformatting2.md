---
title: RequestSendAndForgetNoFormatting2 规则（kmdf）
description: RequestSendAndForgetNoFormatting2 规则验证驱动程序在将请求发送到具有 send 选项 WDF\_请求\_SEND\_选项\_发送的 i/o 目标之前，是否使用 i/o 目标格式设置函数来验证请求的格式\_，\_忘记。
ms.assetid: 1F50CCE7-62A2-44BB-B7B2-86A7AE8EC4CB
ms.date: 05/21/2018
keywords:
- RequestSendAndForgetNoFormatting2 规则（kmdf）
topic_type:
- apiref
api_name:
- RequestSendAndForgetNoFormatting2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 591f6df2d6e4093cb42cf00fe7af06119e690d43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839440"
---
# <a name="requestsendandforgetnoformatting2-rule-kmdf"></a>RequestSendAndForgetNoFormatting2 规则（kmdf）


**RequestSendAndForgetNoFormatting2**规则验证驱动程序在将请求发送到具有 SEND 选项 WDF\_REQUEST\_SEND\_选项的 i/o 目标之前，将验证该驱动程序是否未使用 i/o 目标格式设置函数进行格式设置\_发送\_并忘记\_。

**RequestSendAndForgetNoFormatting2**规则专门检查驱动程序的创建请求。

|              |      |
|--------------|------|
| 驱动程序型号 | KMDF |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>RequestSendAndForgetNoFormatting2</strong>规则。</p>
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
[**WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)
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
 

 





