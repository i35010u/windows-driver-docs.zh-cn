---
title: PdoInitFreeDeviceCreate 规则 (kmdf)
description: PdoInitFreeDeviceCreate 规则指定一个驱动程序必须调用而不是 WdfDeviceCreate WdfDeviceInitFree，如果一个设备对象初始化函数中发生的错误和驱动程序收到 WDFDEVICE\_INIT 结构调用到 WdfPdoInitAllocate。
ms.assetid: d73401dd-ec96-4870-9f6d-aa399deab173
ms.date: 05/21/2018
keywords:
- PdoInitFreeDeviceCreate 规则 (kmdf)
topic_type:
- apiref
api_name:
- PdoInitFreeDeviceCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87b9e76a0037e2ce4e9d02a7a4ceb7aa7b3b8be3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554370"
---
# <a name="pdoinitfreedevicecreate-rule-kmdf"></a>PdoInitFreeDeviceCreate 规则 (kmdf)


**PdoInitFreeDeviceCreate**规则指定一个驱动程序必须调用[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)而不是[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)出错时在一个设备对象初始化函数和驱动程序收到 WDFDEVICE\_调用 INIT 结构[ **WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786).

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>PdoInitFreeDeviceCreate</strong>规则。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)
[**WdfDeviceInitAssignSDDLString** ](https://msdn.microsoft.com/library/windows/hardware/ff546035) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043) 
 [ **WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfDeviceInitRegisterPnpStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546057) 
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)
[**WdfDeviceInitRegisterPowerStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546071)
 [ **WdfPdoInitAddCompatibleID**](https://msdn.microsoft.com/library/windows/hardware/ff548776)
[**WdfPdoInitAddDeviceText** ](https://msdn.microsoft.com/library/windows/hardware/ff548780) 
[ **WdfPdoInitAddHardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff548784)
[**WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786) 
[ **WdfPdoInitAssignDeviceID**](https://msdn.microsoft.com/library/windows/hardware/ff548797)
[**WdfPdoInitAssignInstanceID** ](https://msdn.microsoft.com/library/windows/hardware/ff548799) 
 [ **WdfPdoInitAssignRawDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548802)另请参阅
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**InitFreeDeviceCreateType4** ](kmdf-initfreedevicecreatetype4.md) 
 [ **PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md)
[**PdoInitFreeDeviceCreateType4** ](kmdf-pdoinitfreedevicecreatetype4.md) 
 [ **InitFreeNull**](kmdf-initfreenull.md)
 

 





