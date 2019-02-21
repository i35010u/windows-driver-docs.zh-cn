---
title: 支持功能的电源状态
description: 支持功能的电源状态
ms.assetid: F96214C9-702D-402E-B873-5DF57C521B34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b35c98b3faa551fbdf954c2d2a6ee0d9a24d5ca4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534695"
---
# <a name="supporting-functional-power-states"></a>支持功能的电源状态


从 Windows 8 中，电源管理器包括运行电源管理框架 (PoFx)。 PoFx 支持电源和时钟管理组件 （或子） 级别。

从版本 1.11 KMDF，KMDF 驱动程序可以充分利用 PoFx 提供细粒度的电源控制。 具体而言，KMDF 驱动程序可以定义单个设备，其中每个可进行独立的电源管理中的多个逻辑组件。

例如，功能驱动程序可能会定义一组唯一的设备的每个逻辑组件的功能的电源状态。 类似于设备和系统的电源状态，F0 表示组件完全处于打开状态，同时可选状态 F1，F2，并且等表明渐进式低功率状态。 若要支持 Fx 状态，驱动程序必须在设备的电源策略所有者。

下表总结了 framework 对不同功能的电源状态方案的支持。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">KMDF 支持</th>
<th align="left">UMDF 支持</th>
<th align="left">何时使用/如何对实现</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, single state (F0)](supporting-multiple-functional-power-states-for-single-component-devices.md)">单个组件的单个状态 (F0)</a></p></td>
<td align="left"><p>支持</p></td>
<td align="left"><p>支持</p></td>
<td align="left"><p>当你希望 power 引擎插件 (PEP) 来确定的空闲超时值，并且您的驱动程序具有只有一个 F 状态。</p>
<p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545903" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545903)"> <strong>WdfDeviceAssignS0IdleSettings</strong> </a>与<em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>或<strong>SystemManagedIdleTimoutWithHint</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, multiple states (F0, F1, F2…)](supporting-multiple-functional-power-states-for-single-component-devices.md)">单个组件，多个状态 (...F0，F1，F2)</a></p></td>
<td align="left"><p>支持</p></td>
<td align="left"><p>不支持</p></td>
<td align="left"><p>当您的驱动程序具有多个 F 状态。</p>
<ul>
<li>调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh451097" data-raw-source="[&lt;strong&gt;WdfDeviceWdmAssignPowerFrameworkSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451097)"> <strong>WdfDeviceWdmAssignPowerFrameworkSettings</strong> </a>注册 WDM PoFx 回调。</li>
<li>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545903" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545903)"> <strong>WdfDeviceAssignS0IdleSettings</strong> </a>与<em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>。</li>
</ul>
<p>在这种情况下，KMDF 处理与 PoFx 大多数交互。</p>
<p>有关示例代码，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">PoFx 示例驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-multiple-component-devices.md" data-raw-source="[Multiple components, single or multiple states](supporting-multiple-functional-power-states-for-multiple-component-devices.md)">多个组件、 一个或多个状态</a></p></td>
<td align="left"><p>支持使用 WDM 接口</p></td>
<td align="left"><p>不支持</p></td>
<td align="left"><p>当您的驱动程序具有多个组件。 在这种情况下，必须直接使用 PoFx 接口。</p>
<p>有关示例代码，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">PoFx 示例驱动程序</a>。</p></td>
</tr>
</tbody>
</table>

 

由于 KMDF 增加了基于 PoFx 的最小抽象，最好有 PoFx 写入您的驱动程序之前，对一个基本的了解。 相应地，我们建议您阅读[电源管理框架概述](https://msdn.microsoft.com/library/windows/hardware/hh406637)之前阅读这些主题。

 

 





