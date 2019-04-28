---
title: DeviceInitAllocate 规则 (kmdf)
description: DeviceInitAllocate 规则指定的 PDO 设备或控制的设备对象，必须在之前的驱动程序调用 WdfDeviceCreate 调用方法 WdfPdoInitAllocate 或 WdfControlDeviceInitAllocate framework 设备对象初始化。
ms.assetid: 81bad62a-4bc3-4e34-9634-2a980e1941e5
ms.date: 05/21/2018
keywords:
- DeviceInitAllocate 规则 (kmdf)
topic_type:
- apiref
api_name:
- DeviceInitAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: daf83daef2501ad66da0e1225b4a0d07c8bdd47d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350509"
---
# <a name="deviceinitallocate-rule-kmdf"></a>DeviceInitAllocate 规则 (kmdf)


**DeviceInitAllocate**规则指定，对于 PDO 设备或控制设备对象，该框架设备对象初始化方法[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)或[ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)驱动程序调用前，必须调用[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DeviceInitAllocate</strong>规则。</p>
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
 

 





