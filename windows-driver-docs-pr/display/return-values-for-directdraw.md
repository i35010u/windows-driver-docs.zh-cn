---
title: DirectDraw 的返回值
description: DirectDraw 的返回值
keywords:
- 返回值 WDK DirectDraw
- 绘制 WDK DirectDraw，返回值
- DirectDraw WDK Windows 2000 显示，返回值
- 错误 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c401ff1da842a9d673d39c5de84cbe036c590e
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812575"
---
# <a name="return-values-for-directdraw"></a>DirectDraw 的返回值

下表列出了由 [DirectDraw 驱动程序提供的函数](windows-2000-driver-initialization.md)可返回的值。 在 DWORD 返回值中实际返回 DDHAL_DRIVER_ *Xxx* 值。 DD_OK 值和 DDERR_ *Xxx* 错误代码将在特定函数的参数指向的结构的 **ddRVal** 成员中返回。

有关每个函数可以返回的特定错误代码，请参阅参考部分中的函数说明。 有关错误代码和返回值的完整列表，请参阅 DirectDraw 标头文件 *ddraw* 和 *dxmini* 。 请注意，错误代码由负值表示，不能组合使用。

DirectDraw 驱动程序中的函数必须返回两个返回代码之一： DDHAL_DRIVER_HANDLED 或 DDHAL_DRIVER_NOTHANDLED。 如果驱动程序返回 DDHAL_DRIVER_HANDLED，则它还必须返回 DD_OK 或 *ddraw* 中列出的其中一个错误代码。 DirectDraw 驱动程序中的函数可以返回下表中的代码。 这些代码在 *ddraw* 中定义。

| 返回代码 | 含义 |
| ----------- | ------- |
| DD_OK | 请求已成功完成。 |
| DDHAL_DRIVER_HANDLED | 驱动程序已执行该操作，并在传递给驱动程序的回调的结构的 **ddrval** 成员中返回了该操作的有效返回代码。 如果 DD_OK 此代码，DirectDraw 或 Direct3D 将继续执行该函数。 否则，DirectDraw 或 Direct3D 返回驱动程序提供的错误代码，并中止该函数。 |
| DDHAL_DRIVER_NOCKEYHW | 显示驱动程序无法处理调用，因为它用尽了颜色关键硬件资源。 |
| DDHAL_DRIVER_NOTHANDLED | 驱动程序在请求的操作上没有注释。 如果需要驱动程序实现特定的回调，DirectDraw 或 Direct3D 将报告错误条件。 否则，DirectDraw 或 Direct3D 处理操作，就好像未通过执行 DirectDraw 或 Direct3D 独立于设备的实现来定义驱动程序回调。 DirectDraw 和 Direct3D 通常会忽略回调的参数结构的 **ddrval** 成员中返回的任何值。 |
| DDERR_GENERIC | 出现未定义的错误条件。 |
| DDERR_OUTOFCAPS | 请求的操作所需的硬件已被分配。 |
| DDERR_UNSUPPORTED | 此操作不受支持。 |

在[视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)中实现的[DxApi 函数](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)将返回下表中的其中一个代码。 这些代码在 *dxmini* 中定义。

| 返回代码 | 含义 |
| ----------- | ------- |
| DX_OK | 请求已成功完成。 |
| DXERR_GENERIC | 出现未定义的错误条件。 |
| DXERR_OUTOFCAPS | 请求的操作所需的硬件已被分配。 |
| DXERR_UNSUPPORTED | 此操作不受支持。 |
