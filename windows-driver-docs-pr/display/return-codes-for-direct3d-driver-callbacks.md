---
title: Direct3D 驱动程序回调的返回代码
description: Direct3D 驱动程序回调的返回代码
ms.assetid: 033beb6e-5872-4cb3-8f39-459e2fff82cd
keywords:
- Direct3D WDK Windows 2000 显示，返回代码
- 返回代码 WDK Direct3D
- 回调 WDK Direct3D
- 回调函数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 648b0b275ce799514cc34c7fd39d2bc7842f1e2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522220"
---
# <a name="return-codes-for-direct3d-driver-callbacks"></a>Direct3D 驱动程序回调的返回代码


## <span id="ddk_return_codes_for_direct3d_driver_callbacks_gg"></span><span id="DDK_RETURN_CODES_FOR_DIRECT3D_DRIVER_CALLBACKS_GG"></span>


下表列出了可以返回的值[Direct3D Driver-Supplied 函数](https://msdn.microsoft.com/library/windows/hardware/ff552859)。 DDHAL\_驱动程序\_*Xxx*值实际上返回的 DWORD 返回值。 D3D\_确定的值，D3DHAL\_*Xxx*值和 D3DERR\_*Xxx*中返回的错误代码为**ddrval**的成员特定函数的参数所指向的结构。

有关每个函数可以返回的特定错误代码，请参阅参考部分中的函数和结构描述。 Direct3D 标头文件，请参阅*d3d.h*并*d3dhal.h*有关的错误代码和返回值的完整列表 (此外， *d3d8.h*和*d3d9.h*DirectX 版本 8.0 和 9.0)。 请注意，错误代码都是负值，并且不能结合使用。

Direct3D 驱动程序中的函数必须返回两个返回代码之一：DDHAL\_驱动程序\_HANDLED 或 DDHAL\_驱动程序\_NOTHANDLED。 如果该驱动程序返回 DDHAL\_驱动程序\_处理，则还必须返回任一 D3D\_确定或所列的值之一*d3d.h*或*d3dhal.h*。 Direct3D 驱动程序中的函数可以在下表中返回的值。 这些值中定义*d3d.h*并*d3dhal.h*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D3D_OK （定义为 DD_OK）</p></td>
<td align="left"><p>请求已成功完成。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DHAL_CONTEXT_BAD</p></td>
<td align="left"><p>传入的上下文无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DDHAL_DRIVER_HANDLED</p></td>
<td align="left"><p>驱动程序已执行操作并返回在该操作的有效返回代码<strong>ddrval</strong>结构中的成员传递给驱动程序&#39;s 回调。 如果此代码，D3D_OK Direct3D 继续执行该函数。 否则为 Direct3D 返回驱动程序提供的错误代码，并中止该函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DDHAL_DRIVER_NOTHANDLED</p></td>
<td align="left"><p>该驱动程序上请求的操作有任何注释。 如果该驱动程序需要实现了特定的回调，Direct3D 报告的错误条件。 否则，Direct3D 处理操作，因为如果不通过执行 Direct3D 独立于设备的实现定义的驱动程序回调。 Direct3D 通常会忽略中返回任何值<strong>ddrval</strong>该回叫的成员&#39;s 参数结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D3DHAL_OUTOFCONTEXTS</p></td>
<td align="left"><p>没有在此过程中保留更多上下文。</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3DERR_UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>不支持颜色操作。</p></td>
</tr>
</tbody>
</table>

 

 

 





