---
title: InternalIoctlReqs 规则 (kmdf)
description: InternalIoctlReqs 规则指定内部 IOCTL 请求都不传递到不适合 KMDF 发送的请求的设备驱动程序接口 (DDIs)。
ms.assetid: a6d75752-21eb-486b-b73a-8d810b392e6b
ms.date: 05/21/2018
keywords:
- InternalIoctlReqs 规则 (kmdf)
topic_type:
- apiref
api_name:
- InternalIoctlReqs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09767a2d0c1752db4f40acb006fcb5c0e7a2fe91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546564"
---
# <a name="internalioctlreqs-rule-kmdf"></a>InternalIoctlReqs 规则 (kmdf)


**InternalIoctlReqs**规则指定内部 IOCTL 请求不会传递到不适合 KMDF 发送的请求的设备驱动程序接口 (DDIs)。

提供给 EVT 中的驱动程序的所有请求\_WDF\_IO\_队列\_IO\_内部\_设备\_控制回调函数都保证是内部 IOCTL请求数。 因此，不能通过使用特定于发送读取、 写入或 IOCTL，请求，如 DDIs 发送这些 Ioctl **WdfIoTargetSendReadSynchronously**， **WdfIoTargetSendWriteSynchronously**，**WdfIoTargetSendIoctlSynchronously**， **WdfUsbTargetPipeWriteSynchronously**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>InternalIoctlReqs</strong>规则。</p>
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

[**WdfIoTargetSendIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548660)
[**WdfIoTargetSendReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548669) 
 [ **WdfIoTargetSendWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548672)
[**WdfUsbTargetPipeReadSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551155) 
 [ **WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)
 

 





