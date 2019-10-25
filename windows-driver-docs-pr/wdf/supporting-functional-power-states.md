---
title: 支持功能性电源状态
description: 支持功能性电源状态
ms.assetid: F96214C9-702D-402E-B873-5DF57C521B34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a551255747202404e10beb02d7a49c99e96dcd27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831800"
---
# <a name="supporting-functional-power-states"></a>支持功能性电源状态


从 Windows 8 开始，电源管理器包含运行时电源管理框架（PoFx）。 PoFx 支持组件（或 subdevice）级别的电源和时钟管理。

从 KMDF 1.11 版开始，KMDF 驱动程序可以利用 PoFx 提供的细化电源控制功能。 特别是，KMDF 驱动程序可以在单个设备中定义多个逻辑组件，每个组件都可以独立于电源进行管理。

例如，函数驱动程序可能为设备的每个逻辑组件定义一组独特的功能电源状态。 与设备和系统电源状态类似，F0 指示组件已完全打开，而可选状态 F1、F2 等指示逐渐降低的电源状态。 若要支持 Fx 状态，驱动程序必须是设备的电源策略所有者。

下表汇总了针对不同功能动力状态情况的框架支持。

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
<th align="left">何时使用/如何实现</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, single state (F0)](supporting-multiple-functional-power-states-for-single-component-devices.md)">单个组件，单状态（F0）</a></p></td>
<td align="left"><p>支持</p></td>
<td align="left"><p>支持</p></td>
<td align="left"><p>当你希望 power engine 插件（PEP）确定空闲超时值时，并且你的驱动程序只有一个 F 状态。</p>
<p>通过<em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>或<strong>SystemManagedIdleTimoutWithHint</strong>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-single-component-devices.md" data-raw-source="[Single component, multiple states (F0, F1, F2…)](supporting-multiple-functional-power-states-for-single-component-devices.md)">单个组件，多个状态（F0，F1，F2 ...）</a></p></td>
<td align="left"><p>支持</p></td>
<td align="left"><p>不支持</p></td>
<td align="left"><p>当驱动程序具有多个 F 状态时。</p>
<ul>
<li>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings" data-raw-source="[&lt;strong&gt;WdfDeviceWdmAssignPowerFrameworkSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)"><strong>WdfDeviceWdmAssignPowerFrameworkSettings</strong></a>以注册 WDM PoFx 回调。</li>
<li>通过<em>IdleTimeoutType</em> = <strong>SystemManagedIdleTimout</strong>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a> 。</li>
</ul>
<p>在这种情况下，KMDF 将处理与 PoFx 的大多数交互。</p>
<p>有关示例代码，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">PoFx 示例驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="supporting-multiple-functional-power-states-for-multiple-component-devices.md" data-raw-source="[Multiple components, single or multiple states](supporting-multiple-functional-power-states-for-multiple-component-devices.md)">多个组件，一种或多种状态</a></p></td>
<td align="left"><p>支持使用 WDM 接口</p></td>
<td align="left"><p>不支持</p></td>
<td align="left"><p>当驱动程序具有多个组件时。 在这种情况下，必须直接使用 PoFx 接口。</p>
<p>有关示例代码，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkId=617937" data-raw-source="[PoFx sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=617937)">PoFx 示例驱动程序</a>。</p></td>
</tr>
</tbody>
</table>

 

由于 KMDF 在 PoFx 上添加了最小抽象，因此在编写驱动程序之前，对 PoFx 有一个基本的了解会很有帮助。 因此，建议您阅读以下主题之前，先阅读[电源管理框架概述](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)。

 

 





