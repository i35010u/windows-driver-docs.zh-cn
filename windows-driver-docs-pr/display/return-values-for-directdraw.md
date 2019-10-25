---
title: DirectDraw 的返回值
description: DirectDraw 的返回值
ms.assetid: da4cc7d7-6826-48aa-96c6-004e31fc3e3e
keywords:
- 返回值 WDK DirectDraw
- 绘制 WDK DirectDraw，返回值
- DirectDraw WDK Windows 2000 显示，返回值
- 错误 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba99c2d0e57d6521b9cb167fcccbdf6e6ffbf073
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829565"
---
# <a name="return-values-for-directdraw"></a>DirectDraw 的返回值


## <span id="ddk_return_values_for_directdraw_gg"></span><span id="DDK_RETURN_VALUES_FOR_DIRECTDRAW_GG"></span>


下表列出了由[DirectDraw 驱动程序提供的函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)可返回的值。 DDHAL\_驱动程序\_*Xxx*值实际在 DWORD 返回值中返回。 在特定函数的参数指向的结构的**ddRVal**成员中返回 DD\_OK 值和 DDERR\_*Xxx*错误代码。

有关每个函数可以返回的特定错误代码，请参阅参考部分中的函数说明。 有关错误代码和返回值的完整列表，请参阅 DirectDraw 标头文件*ddraw*和*dxmini* 。 请注意，错误代码由负值表示，不能组合使用。

DirectDraw 驱动程序中的函数必须返回两个返回代码之一： DDHAL\_驱动程序\_处理或 DDHAL\_驱动程序\_NOTHANDLED。 如果驱动程序返回 DDHAL\_驱动程序\_处理，则它还必须返回 DD\_"确定" 或*ddraw*中列出的错误代码之一。 DirectDraw 驱动程序中的函数可以返回下表中的代码。 这些代码在*ddraw*中定义。

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
<td align="left"><p>驱动程序已执行该操作，并在传递给驱动程序的回调的结构的<strong>ddrval</strong>成员中返回了该操作的有效返回代码。 如果此代码为 DD_OK，DirectDraw 或 Direct3D 将继续执行该函数。 否则，DirectDraw 或 Direct3D 返回驱动程序提供的错误代码，并中止该函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDHAL_DRIVER_NOCKEYHW</p></td>
<td align="left"><p>显示驱动程序无法处理调用，因为它用尽了颜色关键硬件资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>驱动程序在请求的操作上没有注释。 如果需要驱动程序实现特定的回调，DirectDraw 或 Direct3D 将报告错误条件。 否则，DirectDraw 或 Direct3D 处理操作，就好像未通过执行 DirectDraw 或 Direct3D 独立于设备的实现来定义驱动程序回调。 DirectDraw 和 Direct3D 通常会忽略回调的参数结构的<strong>ddrval</strong>成员中返回的任何值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_GENERIC</p></td>
<td align="left"><p>出现未定义的错误条件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDERR_OUTOFCAPS</p></td>
<td align="left"><p>请求的操作所需的硬件已被分配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDERR_UNSUPPORTED</p></td>
<td align="left"><p>不支持该操作。</p></td>
</tr>
</tbody>
</table>

 

在[视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)中实现的[DxApi 函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)将返回下表中的其中一个代码。 这些代码在*dxmini*中定义。

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
<td align="left"><p>出现未定义的错误条件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXERR_OUTOFCAPS</p></td>
<td align="left"><p>请求的操作所需的硬件已被分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXERR_UNSUPPORTED</p></td>
<td align="left"><p>不支持该操作。</p></td>
</tr>
</tbody>
</table>

 

 

 





