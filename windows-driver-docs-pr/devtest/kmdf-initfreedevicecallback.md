---
title: InitFreeDeviceCallback 规则 (kmdf)
description: InitFreeDeviceCallback 规则指定如果驱动程序时遇到错误时它可以初始化新的 framework 设备对象，和驱动程序收到 WDFDEVICE 驱动程序，必须调用 WdfDeviceInitFree\_调用 INIT 结构WdfControlDeviceInitAllocate。
ms.assetid: 518f60cf-283a-4924-8bbd-2f5e26d3e850
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCallback 规则 (kmdf)
topic_type:
- apiref
api_name:
- InitFreeDeviceCallback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f4d63598cac4ae13253d148c5ae31ba9f5bd0da5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340307"
---
# <a name="initfreedevicecallback-rule-kmdf"></a>InitFreeDeviceCallback 规则 (kmdf)


InitFreeDeviceCallback 规则指定一个驱动程序必须调用[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)如果驱动程序时遇到错误时它可以初始化新的 framework 设备对象，和驱动程序收到[ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)调用结构[ **WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>InitFreeDeviceCallback</strong>规则。</p>
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

[**WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)
[**WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029) 
 [ **WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)
[**WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043) 
 [**WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfDeviceInitRegisterPnpStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546057) 
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)
[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546071) 
 [ **WdfPdoInitAddCompatibleID**](https://msdn.microsoft.com/library/windows/hardware/ff548776)
[**WdfPdoInitAddDeviceText** ](https://msdn.microsoft.com/library/windows/hardware/ff548780)
 [ **WdfPdoInitAddHardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff548784)
[**WdfPdoInitAssignDeviceID** ](https://msdn.microsoft.com/library/windows/hardware/ff548797)
 [ **WdfPdoInitAssignInstanceID**](https://msdn.microsoft.com/library/windows/hardware/ff548799)
[**WdfPdoInitAssignRawDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548802)
 

 





