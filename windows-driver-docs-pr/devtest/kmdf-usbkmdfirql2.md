---
title: UsbKmdfIrql2 规则 (kmdf)
description: UsbKmdfIrql2 规则指定 KMDF 驱动程序应在不正确的 IRQL 级别调用特定于 USB 的 DDIs。
ms.assetid: D514B902-8F29-4D77-A26F-57DA43A045E8
ms.date: 05/21/2018
keywords:
- UsbKmdfIrql2 规则 (kmdf)
topic_type:
- apiref
api_name:
- UsbKmdfIrql2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c24ecae95639abcbafc7909fc5ca1a8ab6a20e17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547330"
---
# <a name="usbkmdfirql2-rule-kmdf"></a>UsbKmdfIrql2 规则 (kmdf)


**UsbKmdfIrql2**规则指定，KMDF 驱动程序不应调用特定于 USB 的 DDIs 不正确的 IRQL 在级别。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>UsbKmdfIrql2</strong>规则。</p>
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

[**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)
[**WdfUsbInterfaceGetConfiguredSettingIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff550059) 
 [ **WdfUsbInterfaceGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550060)
[**WdfUsbInterfaceGetEndpointInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff550063) 
 [**WdfUsbInterfaceGetInterfaceNumber**](https://msdn.microsoft.com/library/windows/hardware/ff550065)
[**WdfUsbInterfaceGetNumConfiguredPipes** ](https://msdn.microsoft.com/library/windows/hardware/ff550066) 
[ **WdfUsbInterfaceGetNumEndpoints**](https://msdn.microsoft.com/library/windows/hardware/ff550068)
[**WdfUsbInterfaceGetNumSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff550070) 
 [ **WdfUsbInterfaceSelectSetting**](https://msdn.microsoft.com/library/windows/hardware/ff550073)
[**WdfUsbTargetDeviceAllocAndQueryString** ](https://msdn.microsoft.com/library/windows/hardware/ff550074)
 [ **WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)
[**WdfUsbTargetDeviceCyclePortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550080) 
 [ **WdfUsbTargetDeviceFormatRequestForControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff550082) 
 [ **WdfUsbTargetDeviceFormatRequestForCyclePort**](https://msdn.microsoft.com/library/windows/hardware/ff550084)
[**WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086)
 [ **WdfUsbTargetDeviceFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff550088) 
 [ **WdfUsbTargetDeviceGetDeviceDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550090)
[**WdfUsbTargetDeviceGetInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550092) 
 [ **WdfUsbTargetDeviceGetNumInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff550094)
[**WdfUsbTargetDeviceIsConnectedSynchronous** ](https://msdn.microsoft.com/library/windows/hardware/ff550095) 
 [ **WdfUsbTargetDeviceQueryString** ](https://msdn.microsoft.com/library/windows/hardware/ff550096) 
 [ **WdfUsbTargetDeviceResetPortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550097)
[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550098)
**](https://msdn.microsoft.com/library/windows/hardware/ff551163)
 

 





