---
title: DirectDraw 的返回值
description: DirectDraw 的返回值
ms.assetid: da4cc7d7-6826-48aa-96c6-004e31fc3e3e
keywords:
- 返回值 WDK DirectDraw
- 绘制 WDK DirectDraw，返回值
- DirectDraw WDK Windows 2000 显示，则返回值
- 错误 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d48e53198895471f1dd06b011f885ad5682c3d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349496"
---
# <a name="return-values-for-directdraw"></a>DirectDraw 的返回值


## <span id="ddk_return_values_for_directdraw_gg"></span><span id="DDK_RETURN_VALUES_FOR_DIRECTDRAW_GG"></span>


下面的表可以返回的列表值[DirectDraw 驱动程序提供的函数](https://msdn.microsoft.com/library/windows/hardware/ff553833)。 DDHAL\_驱动程序\_*Xxx*值实际上返回的 DWORD 返回值。 DD\_确定的值和 DDERR\_*Xxx*中返回错误代码**ddRVal**特定函数的参数所指向的结构的成员。

有关每个函数可以返回的特定错误代码，请参阅参考部分中的函数描述。 DirectDraw 标头文件，请参阅*ddraw.h*并*dxmini.h*有关的错误代码和返回值的完整列表。 请注意，错误代码都是负值，并且不能结合使用。

DirectDraw 驱动程序中的函数必须返回两个返回代码之一：DDHAL\_驱动程序\_HANDLED 或 DDHAL\_驱动程序\_NOTHANDLED。 如果该驱动程序返回 DDHAL\_驱动程序\_处理，则还必须返回两 DD\_中列出的确定或错误代码之一*ddraw.h*。 DirectDraw 驱动程序中的函数可以返回以下表中的代码。 这些代码中定义*ddraw.h*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DD_OK</p></td>
<td align="left"><p>请求已成功完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_HANDLED</p></td>
<td align="left"><p>驱动程序已执行操作并返回在该操作的有效返回代码<strong>ddrval</strong>结构中的成员传递给驱动程序的回调。 如果此代码，DD_OK DirectDraw 或 Direct3D 继续执行该函数。 否则为 DirectDraw 或 Direct3D 返回驱动程序提供的错误代码，将中止该函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDHAL_DRIVER_NOCKEYHW</p></td>
<td align="left"><p>显示驱动程序无法处理该呼叫，因为它已耗尽颜色键的硬件资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>该驱动程序上请求的操作有任何注释。 如果该驱动程序需要实现了特定的回调，DirectDraw 或 Direct3D 报告的错误条件。 否则，DirectDraw 或 Direct3D 处理操作，因为如果不通过执行 DirectDraw 或 Direct3D 独立于设备的实现定义的驱动程序回调。 DirectDraw 和 Direct3D 通常忽略中返回任何值<strong>ddrval</strong>该回调的参数结构的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_GENERIC</p></td>
<td align="left"><p>没有未定义的错误条件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDERR_OUTOFCAPS</p></td>
<td align="left"><p>已分配请求的操作所需的硬件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_UNSUPPORTED</p></td>
<td align="left"><p>不支持该操作。</p></td>
</tr>
</tbody>
</table>

 

一个[DxApi 函数](https://msdn.microsoft.com/library/windows/hardware/ff557387)中实现[微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)下表中返回代码之一。 这些代码中定义*dxmini.h*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DX_OK</p></td>
<td align="left"><p>请求已成功完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXERR_GENERIC</p></td>
<td align="left"><p>没有未定义的错误条件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXERR_OUTOFCAPS</p></td>
<td align="left"><p>已分配请求的操作所需的硬件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXERR_UNSUPPORTED</p></td>
<td align="left"><p>不支持该操作。</p></td>
</tr>
</tbody>
</table>

 

 

 





