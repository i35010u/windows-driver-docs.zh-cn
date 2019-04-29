---
title: IoBuildDeviceIoControlSetEvent 规则 (wdm)
description: IoBuildDeviceIoControlSetEvent 规则指定是否驱动程序提供指向调用方分配并初始化事件对象的指针，调用 IoBuildDeviceIoControlRequest 的驱动程序必须不调用 KeSetEvent。
ms.assetid: F9721484-3156-4AF5-8C60-AF68644E602D
ms.date: 05/21/2018
keywords:
- IoBuildDeviceIoControlSetEvent 规则 (wdm)
topic_type:
- apiref
api_name:
- IoBuildDeviceIoControlSetEvent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08837c3b2b514113d433167af25ccfa978c445a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362631"
---
# <a name="iobuilddeviceiocontrolsetevent-rule-wdm"></a>IoBuildDeviceIoControlSetEvent 规则 (wdm)


**IoBuildDeviceIoControlSetEvent**规则指定的调用驱动程序[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)不能调用[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)如果驱动程序提供指向调用方分配并初始化事件对象的指针。 **KeSetEvent**不需要为此 IRP 的调用由驱动程序。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoBuildDeviceIoControlSetEvent</strong>规则。</p>
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

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**KeClearEvent**](https://msdn.microsoft.com/library/windows/hardware/ff551980)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
[**KeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553253)
 

 





