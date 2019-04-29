---
title: IoBuildDeviceControlNoFree 规则 (wdm)
description: IoBuildDeviceControlNoFree 规则指定调用 IoBuildDeviceIoControlRequest 的驱动程序必须调用 IoFreeIrp。
ms.assetid: 36DAB9A8-2B6F-43EE-86CC-97B66FE0AEB8
ms.date: 05/21/2018
keywords:
- IoBuildDeviceControlNoFree 规则 (wdm)
topic_type:
- apiref
api_name:
- IoBuildDeviceControlNoFree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4cd089852424a3945455bb7c84aa57ad8c0585f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362824"
---
# <a name="iobuilddevicecontrolnofree-rule-wdm"></a>IoBuildDeviceControlNoFree 规则 (wdm)


**IoBuildDeviceControlNoFree**规则指定的调用驱动程序[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)不能调用[ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)。

调用的驱动程序[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)不能调用[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)因为 I/O 管理器释放这些同步后的 Irp [ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)已调用。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoBuildDeviceControlNoFree</strong>规则。</p>
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
[**IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)
 

 





