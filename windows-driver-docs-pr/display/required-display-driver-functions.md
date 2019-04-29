---
title: 必需的显示驱动程序函数
description: 必需的显示驱动程序函数
ms.assetid: 483aa13b-a14d-49f3-8265-013f7bb64d40
keywords:
- 显示图形 DDI 函数 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e78c22763f499f34720b102834224ff6539976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383222"
---
# <a name="required-display-driver-functions"></a>必需的显示驱动程序函数


## <span id="ddk_required_display_driver_functions_gg"></span><span id="DDK_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


至少，每个显示器驱动程序，必须：

1.  启用和禁用图形硬件。

2.  GDI 提供硬件功能信息。

3.  启用的绘图图面。

下表列出了所有显示驱动程序的函数必须实现。 遵循**DrvEnableDriver**，其余函数按字母顺序列出。 请注意，除**DrvEnableDriver**、 哪些 GDI 调用按名称、 所有其他显示器驱动程序函数不具有固定的名称，以及与 pseudonames 列出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556210" data-raw-source="[&lt;strong&gt;DrvEnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556210)"><strong>DrvEnableDriver</strong></a></p></td>
<td align="left"><p>作为初始驱动程序入口点，提供了 GDI 的驱动程序版本支持的可选函数的数量和入口点。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556178" data-raw-source="[&lt;strong&gt;DrvAssertMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556178)"><strong>DrvAssertMode</strong></a></p></td>
<td align="left"><p>重置为指定的视频硬件设备的视频模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556181" data-raw-source="[&lt;strong&gt;DrvCompletePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556181)"><strong>DrvCompletePDEV</strong></a></p></td>
<td align="left"><p>通知完成设备安装驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556196" data-raw-source="[&lt;strong&gt;DrvDisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556196)"><strong>DrvDisableDriver</strong></a></p></td>
<td align="left"><p>释放所有已分配的资源的驱动程序并将设备返回到其最初加载状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556198" data-raw-source="[&lt;strong&gt;DrvDisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556198)"><strong>DrvDisablePDEV</strong></a></p></td>
<td align="left"><p>当不再需要硬件时，将释放内存和资源使用的设备和创建，但尚未删除的任何图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556200" data-raw-source="[&lt;strong&gt;DrvDisableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556200)"><strong>DrvDisableSurface</strong></a></p></td>
<td align="left"><p>告知驱动程序不再需要为当前的设备创建的面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556211" data-raw-source="[&lt;strong&gt;DrvEnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556211)"><strong>DrvEnablePDEV</strong></a></p></td>
<td align="left"><p>使<a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-pdev" data-raw-source="&lt;em&gt;PDEV&lt;/em&gt;"> <em>PDEV</em></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556214" data-raw-source="[&lt;strong&gt;DrvEnableSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556214)"><strong>DrvEnableSurface</strong></a></p></td>
<td align="left"><p>创建用于指定的硬件设备的面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556233" data-raw-source="[&lt;strong&gt;DrvGetModes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556233)"><strong>DrvGetModes</strong></a></p></td>
<td align="left"><p>列出指定视频硬件设备支持的模式。</p></td>
</tr>
</tbody>
</table>

 

所需的所有图形驱动程序的功能列表将显示在[所需的图形驱动程序函数](required-graphics-driver-functions.md)。

 

 





