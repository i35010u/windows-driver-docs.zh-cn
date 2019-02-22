---
title: 所需的图形驱动程序函数
description: 所需的图形驱动程序函数
ms.assetid: 3a7a7516-b758-4499-bd9d-216fef7b3c8c
keywords:
- GDI WDK Windows 2000 显示函数所需
- 显示图形驱动程序 WDK Windows 2000，所需的功能
- 所需功能 WDK 图形
- 所需的绘图 WDK GDI，函数
- GDI WDK Windows 2000 显示，DDI 所需的函数
- 驱动程序 WDK Windows 2000 显示图形 DDI 所需的功能
- DDI WDK 图形，所需的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb2a2fedb67a7d05f282857cd9af90ee514823f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520566"
---
# <a name="required-graphics-driver-functions"></a>所需的图形驱动程序函数


## <span id="ddk_required_graphics_driver_functions_gg"></span><span id="DDK_REQUIRED_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


所有图形驱动程序必须都支持 GDI 调用来启用和禁用该驱动程序的入口点*PDEV*结构和关联与每个 PDEV 的图面。 下表列出了在其中它们通常被称为顺序所需的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">入口点</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556210" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556210)"><strong>DrvEnableDriver</strong></a></p></td>
<td align="left"><p>作为初始驱动程序入口点，此函数提供 GDI 驱动程序版本支持的可选函数的数量和入口点。 这也是按名称调用 GDI 的唯一驱动程序函数。 所有其他驱动程序函数的函数指针表可以通过访问。 与不同<strong>DrvEnableDriver</strong>，不固定的其他驱动程序函数的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556233" data-raw-source="[&lt;strong&gt;DrvGetModes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556233)"><strong>DrvGetModes</strong></a></p></td>
<td align="left"><p>列出指定视频硬件设备支持的模式。 （此函数是必需的显示器驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556211" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556211)"><strong>DrvEnablePDEV</strong></a></p></td>
<td align="left"><p>使 PDEV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556181" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556181)"><strong>DrvCompletePDEV</strong></a></p></td>
<td align="left"><p>通知的设备安装完成后的驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556214" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556214)"><strong>DrvEnableSurface</strong></a></p></td>
<td align="left"><p>创建用于指定的硬件设备的面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556200" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556200)"><strong>DrvDisableSurface</strong></a></p></td>
<td align="left"><p>告知驱动程序不再需要为当前的设备创建的面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556198" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556198)"><strong>DrvDisablePDEV</strong></a></p></td>
<td align="left"><p>当不再需要硬件时，将释放内存和资源使用的设备和创建，但尚未删除的任何图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556196" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556196)"><strong>DrvDisableDriver</strong></a></p></td>
<td align="left"><p>释放所有已分配的资源的驱动程序并将设备返回到其初始状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556178" data-raw-source="[&lt;strong&gt;DrvAssertMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556178)"><strong>DrvAssertMode</strong></a></p></td>
<td align="left"><p>重置为指定的硬件设备的视频模式。 （此函数是必需的显示器驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556275" data-raw-source="[&lt;strong&gt;DrvResetDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556275)"><strong>DrvResetDevice</strong></a></p></td>
<td align="left"><p>将设备重置时该数据库已变为不可操作或无响应。</p></td>
</tr>
</tbody>
</table>

 

 

 





