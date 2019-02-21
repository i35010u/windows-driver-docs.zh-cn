---
title: CtlDeviceFinishInitDrEntry 规则 (kmdf)
description: CtlDeviceFinishInitDrEntry 规则指定，是否驱动程序在 DriverEntry 回调函数中创建控制设备对象，它必须调用 WdfControlFinishInitializing，创建设备后，它从 EvtDriverDeviceAdd 退出之前回调函数。 此规则不适用于非 PnP 驱动程序。
ms.assetid: b6470bc1-c4db-4b46-b83b-edcf4da56087
ms.date: 05/21/2018
keywords:
- CtlDeviceFinishInitDrEntry 规则 (kmdf)
topic_type:
- apiref
api_name:
- CtlDeviceFinishInitDrEntry
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c50b673a8d99adbd853cd7ea70bc399451486bc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540388"
---
# <a name="ctldevicefinishinitdrentry-rule-kmdf"></a>CtlDeviceFinishInitDrEntry 规则 (kmdf)


CtlDeviceFinishInitDrEntry 规则指定如果驱动程序创建中的控制设备对象[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)回调函数，它必须调用[ **WdfControlFinishInitializing** ](https://msdn.microsoft.com/library/windows/hardware/ff545854)创建设备后，它从退出之前[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 此规则不适用于非 PnP 驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>CtlDeviceFinishInitDrEntry</strong>规则。</p>
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

[**WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)
[**WdfControlFinishInitializing**](https://msdn.microsoft.com/library/windows/hardware/ff545854)
[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
 

 





