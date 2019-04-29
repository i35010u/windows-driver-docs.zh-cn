---
title: ControlDeviceDeleted 规则 (kmdf)
description: ControDeviceDeleted 规则指定是否即插即用驱动程序创建一个控制设备对象，该驱动程序必须删除中的一个驱动程序卸载之前清理回调函数的控制设备对象。
ms.assetid: 869f1c1c-8a9f-4e0b-bcbb-386e93663567
ms.date: 05/21/2018
keywords:
- ControlDeviceDeleted 规则 (kmdf)
topic_type:
- apiref
api_name:
- ControlDeviceDeleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08a58b94352f3c5e2171940cb9ea553da921d8ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356448"
---
# <a name="controldevicedeleted-rule-kmdf"></a>ControlDeviceDeleted 规则 (kmdf)


ControDeviceDeleted 规则指定是否即插即用驱动程序创建一个控制设备对象，该驱动程序必须删除中的一个驱动程序卸载之前清理回调函数的控制设备对象。

如果 FDO 或筛选器的驱动程序调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)对于控制设备对象，该驱动程序必须调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)为控制设备对象从 WDFDEVICE 对象，WDFDEVICE 对象销毁回调功能的驱动程序的清理回调函数或[ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)事件的回调函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ControlDeviceDeleted</strong>规则。</p>
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
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
 

 





