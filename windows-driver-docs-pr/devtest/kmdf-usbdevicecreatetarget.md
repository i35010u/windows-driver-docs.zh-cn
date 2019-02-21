---
title: UsbDeviceCreateTarget 规则 (kmdf)
description: UsbDeviceCreateTarget 规则指定设备上下文中当前存在的 WDFUSBDEVICE 对象会泄漏时，会创建多个 WDFUSBDEVICE 对象。
ms.assetid: c2617c2b-553e-44fa-abd5-6bfe6d545612
ms.date: 05/21/2018
keywords:
- UsbDeviceCreateTarget 规则 (kmdf)
topic_type:
- apiref
api_name:
- UsbDeviceCreateTarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be8603547204b01d95b7df25c4bfa19c36f42e38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525927"
---
# <a name="usbdevicecreatetarget-rule-kmdf"></a>UsbDeviceCreateTarget 规则 (kmdf)


**UsbDeviceCreateTarget**规则指定设备上下文中当前存在的 WDFUSBDEVICE 对象会泄漏时，会创建多个 WDFUSBDEVICE 对象。

例如， [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)事件回调函数可以多次调用时系统尝试管理资源和需要分配的内存的不同区块驱动程序。 在此情况下， [ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)事件回调函数调用以取消映射内存资源，framework 最初已调用后*EvtDevicePrepareHardware*. *EvtDevicePrepareHardware*然后再次调用以将资源映射，以便该驱动程序可以访问分配给设备的内存。 此规则检查驱动程序首先验证目标是 WDFUSBDEVICE **NULL**并不只是创建新的设备和替换上一个句柄。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>UsbDeviceCreateTarget</strong>规则。</p>
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

[**WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)
[**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)
 

 





