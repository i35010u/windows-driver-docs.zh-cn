---
title: 强制的目标与连接的目标
description: 强制的目标与连接的目标
ms.assetid: 690e585b-3c90-4373-844d-42afe033b59b
keywords:
- 连接显示 WDK Windows 7 显示 CCD 概念，强制与连接的目标
- 连接显示 WDK Windows Server 2008 R2 显示 CCD 概念，强制与连接的目标
- 配置显示 WDK Windows 7 显示 CCD 概念，强制与连接的目标
- 配置显示 WDK Windows Server 2008 R2 显示 CCD 概念，强制与连接的目标
- CCD 概念 WDK Windows 7 显示，强制与连接的目标
- CCD 概念 WDK Windows Server 2008 R2 显示，强制与连接的目标
- 强制与连接的目标 WDK Windows 7 显示
- 强制与连接的目标 WDK Windows Server 2008 R2 显示
- 强制的目标 WDK Windows 7 显示与连接
- 强制的目标 WDK Windows Server 2008 R2 显示与连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ddc82180342a83e267e4d2583e6fe55e8667916
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576583"
---
# <a name="forced-versus-connected-targets"></a>强制的目标与连接的目标


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

CCD Api 引入已连接的监视器和 forceable 目标的概念。 监视器已连接到目标，如果 GPU 可检测的状态的监视器，这是监视器和目标的物理属性。 目标是 forceable 如果 GPU 可以发送带目标显示信号，即使 GPU 无法检测到已连接的监视器。 所有模拟的目标类型被视为 forceable，并且所有数字目标不会考虑 forceable。 下表介绍连接和强制状态的组合路径处于活动状态且未处于活动状态时。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">路径活动状态</th>
<th align="left">路径强制状态</th>
<th align="left">监视连接状态</th>
<th align="left">结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>活跃</p></td>
<td align="left"><p>强制</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>启用目标的输出，因为监视器连接和处于活动状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>活跃</p></td>
<td align="left"><p>强制</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>目标输出已启用了与路径正在强制和处于活动状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>活跃</p></td>
<td align="left"><p>不强制执行</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>启用目标的输出，因为监视器连接和处于活动状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>活跃</p></td>
<td align="left"><p>不强制执行</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>无法设置路径，因为不强制和监视器不建立连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>未处于活动状态</p></td>
<td align="left"><p>强制</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>可以启用目标的输出，因为正在强制和连接监视器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>未处于活动状态</p></td>
<td align="left"><p>强制</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>可以启用目标的输出，因为正在强制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>未处于活动状态</p></td>
<td align="left"><p>不强制执行</p></td>
<td align="left"><p>已连接</p></td>
<td align="left"><p>可以启用目标的输出，因为连接监视器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>未处于活动状态</p></td>
<td align="left"><p>不强制执行</p></td>
<td align="left"><p>未连接</p></td>
<td align="left"><p>不能启用目标的输出，因为监视器未连接，且不强制执行路径。</p></td>
</tr>
</tbody>
</table>

 

下表介绍了几种类型的可能的强制状态的每个路径。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">强制的状态</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>正常强制</p></td>
<td align="left"><p>这强制状态后 power 转换，重新启动后，将会丢失或强制的状态处于关闭状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>路径持久性</p></td>
<td align="left"><p>这强制状态重新启动后会丢失。 Microsoft Win32 <strong>ChangeDisplaySettingsEx</strong>函数在即使其路径中的这些监视器的目标始终会销毁所有路径保存监视器<strong>ChangeDisplaySettingsEx</strong>调用。 如果调用方调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff569533" data-raw-source="[&lt;strong&gt;SetDisplayConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569533)"> <strong>SetDisplayConfig</strong> </a> CCD 函数中设置的 SDC_USE_SUPPLIED_DISPLAY_CONFIG 或 SDC_TOPOLOGY_SUPPLIED 标志<em>标志</em>参数，则<strong>SetDisplayConfig</strong>将删除保留在路径的监视器。 如果在新的拓扑不包括此监视器处于的路径。 中的所有其他 SDC_TOPOLOGY_XXX 标志指定调用方<em>标志</em>参数， <strong>SetDisplayConfig</strong>中删除保留在路径的监视器，除非调用方还指定 SDC_PATH_PERSIST_新的拓扑结构中处于活动状态 IF_REQUIRED 标志和路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>启动持久性</p></td>
<td align="left"><p>这强制状态只会丢失时处于关闭状态。 在系统重新启动后，此状态是持久性的。</p></td>
</tr>
</tbody>
</table>

 

 

 





