---
title: RequestSendAndForgetNoFormatting2 规则 (kmdf)
description: RequestSendAndForgetNoFormatting2 规则验证该驱动程序不会格式化 I/O 目标格式设置函数中将其发送到发送选项 WDF I/O 目标之前使用的请求\_请求\_发送\_选项\_发送\_AND\_遗忘。
ms.assetid: 1F50CCE7-62A2-44BB-B7B2-86A7AE8EC4CB
ms.date: 05/21/2018
keywords:
- RequestSendAndForgetNoFormatting2 规则 (kmdf)
topic_type:
- apiref
api_name:
- RequestSendAndForgetNoFormatting2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b8facb50ac3980555577dabbd295b1e8a4a3837
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543675"
---
# <a name="requestsendandforgetnoformatting2-rule-kmdf"></a>RequestSendAndForgetNoFormatting2 规则 (kmdf)


**RequestSendAndForgetNoFormatting2**规则将验证该驱动程序不会格式化 I/O 目标格式设置函数中将其发送到发送选项 WDF I/O 目标之前使用的请求\_请求\_发送\_选项\_发送\_AND\_遗忘。

**RequestSendAndForgetNoFormatting2**规则专门检查驱动程序创建请求。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>RequestSendAndForgetNoFormatting2</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfIoTargetFormatRequestForInternalIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff548595)
[**WdfIoTargetFormatRequestForInternalIoctlOthers** ](https://msdn.microsoft.com/library/windows/hardware/ff548599) 
 [**WdfIoTargetFormatRequestForIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff548604)
[**WdfIoTargetFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff548612) 
 [**WdfIoTargetFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff548620)
[**WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951) 
 [ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfUsbTargetDeviceFormatRequestForControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff550082) 
 [ **WdfUsbTargetDeviceFormatRequestForCyclePort**](https://msdn.microsoft.com/library/windows/hardware/ff550084)
[**WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086) 
 [**WdfUsbTargetDeviceFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff550088)
[**WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132) 
 [ **WdfUsbTargetPipeFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff551136) 
 [ **WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138)
[**WdfUsbTargetPipeFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff551139) 
 [ **WdfUsbTargetPipeFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff551141)
 

 





