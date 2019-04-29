---
title: RequestFormattedValid 规则 (kmdf)
description: RequestFormattedValid 规则指定驱动程序设置格式的所有请求，除了 WDF\_请求\_发送\_选项\_发送\_AND\_忘记请求，再发送它们到 I/O 的目标。
ms.assetid: b7da37ed-3ca5-472e-a915-82674c9efee3
ms.date: 05/21/2018
keywords:
- RequestFormattedValid 规则 (kmdf)
topic_type:
- apiref
api_name:
- RequestFormattedValid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0bb089a7564ce894d5b1b90eb2ff499587ec664f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362662"
---
# <a name="requestformattedvalid-rule-kmdf"></a>RequestFormattedValid 规则 (kmdf)


**RequestFormattedValid**规则指定驱动程序设置格式的所有请求，除了 WDF\_请求\_发送\_选项\_发送\_AND\_忘记请求，它将它们发送到的 I/O 目标之前。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>RequestFormattedValid</strong>规则。</p>
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

<a name="applies-to"></a>适用对象
----------

[**WdfIoTargetFormatRequestForInternalIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff548595)
[**WdfIoTargetFormatRequestForInternalIoctlOthers** ](https://msdn.microsoft.com/library/windows/hardware/ff548599) 
 [**WdfIoTargetFormatRequestForIoctl**](https://msdn.microsoft.com/library/windows/hardware/ff548604)
[**WdfIoTargetFormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff548612) 
 [**WdfIoTargetFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff548620)
[**WdfRequestFormatRequestUsingCurrentType** ](https://msdn.microsoft.com/library/windows/hardware/ff549955) 
[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfRequestWdmFormatUsingStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550036) 
[ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082)
[**WdfUsbTargetDeviceFormatRequestForCyclePort** ](https://msdn.microsoft.com/library/windows/hardware/ff550084) 
 [ **WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086) 
 [ **WdfUsbTargetDeviceFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff550088)
[**WdfUsbTargetPipeFormatRequestForAbort** ](https://msdn.microsoft.com/library/windows/hardware/ff551132) 
[ **WdfUsbTargetPipeFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff551136)
[**WdfUsbTargetPipeFormatRequestForReset**](https://msdn.microsoft.com/library/windows/hardware/ff551138) 
 [ **WdfUsbTargetPipeFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff551139) 
 [ **WdfUsbTargetPipeFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff551141)
 

 





