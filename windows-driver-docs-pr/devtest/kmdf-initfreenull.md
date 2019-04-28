---
title: InitFreeNull 规则 (kmdf)
description: InitFreeNull 规则指定 DDIs 接收 PWDFDEVICE\_不能使用 NULL 指针 WDFDEVICE 调用作为参数的 INIT\_INIT 结构。
ms.assetid: 99ced415-9af9-4d06-a10f-4c960897ad5f
ms.date: 05/21/2018
keywords:
- InitFreeNull 规则 (kmdf)
topic_type:
- apiref
api_name:
- InitFreeNull
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0fa7da6ddcea1cd1273a44f941efccc091fbbe79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350390"
---
# <a name="initfreenull-rule-kmdf"></a>InitFreeNull 规则 (kmdf)


**InitFreeNull**规则指定 DDIs 接收 PWDFDEVICE\_不能使用调用作为参数的 INIT **NULL**指向[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。

框架提供方法初始化[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。 当驱动程序调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)若要创建的功能的设备对象 (FDO) 或物理设备对象 (PDO) **WdfDeviceCreate**方法设置第一个参数**NULL**如果它成功。

如果该驱动程序遇到错误时它调用的设备对象初始化方法或[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)，驱动程序必须调用 WdfDeviceInitFree。 后 WdfDeviceInitFree 在成功调用，您应将指针设置为[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构**NULL** (PWDFDEVICE\_INIT =**NULL**).

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>InitFreeNull</strong>规则。</p>
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
[**WdfPdoInitAssignDeviceID** ](https://msdn.microsoft.com/library/windows/hardware/ff548797)
 [ **WdfPdoInitAssignInstanceID**](https://msdn.microsoft.com/library/windows/hardware/ff548799)
[**WdfPdoInitAssignRawDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548802)另请参阅
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**InitFreeDeviceCreateType4** ](kmdf-initfreedevicecreatetype4.md) 
 [ **PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md)
[**PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md) 
 [ **PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md)
 

 





