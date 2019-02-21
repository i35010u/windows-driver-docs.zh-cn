---
title: IoctlReqs 规则 (kmdf)
description: IoctlReqs 规则指定 IOCTL 请求必须不能传递给不适当 KMDF 请求或发送设备驱动程序接口 (DDIs)。
ms.assetid: f13aef5a-61e7-4b99-b86e-e1857de3c2f1
ms.date: 05/21/2018
keywords:
- IoctlReqs 规则 (kmdf)
topic_type:
- apiref
api_name:
- IoctlReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9785c34c936bfe0909b96357f60cd2fa0abe29ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545008"
---
# <a name="ioctlreqs-rule-kmdf"></a>IoctlReqs 规则 (kmdf)


**IoctlReqs**规则指定 IOCTL 请求必须不能传递给不适当 KMDF 请求或发送设备驱动程序接口 (DDIs)。

提供给驱动程序的所有请求[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)事件回调函数都保证是 IOCTL 请求。 在驱动程序*EvtIoDeviceControl*函数声明使用 EVT\_WDF\_IO\_队列\_IO\_设备\_控件函数角色类型声明。

无法将这些 IOCTL 请求发送到特定于发送读取以下 DDIs，写入或 IOCTL 请求：

[**WdfUsbTargetPipeSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551158)， [ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)， [ **WdfIoTargetSendWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548672)， [ **WdfIoTargetSendInternalIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548656)， [ **WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)， [ **WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)， [ **WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoctlReqs</strong>规则。</p>
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

[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548651)
[**WdfIoTargetSendInternalIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548656) 
 [ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)
[**WdfIoTargetSendWriteSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548672) 
[ **WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)
[**WdfUsbTargetPipeSendUrbSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551158)
 [ **WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)








