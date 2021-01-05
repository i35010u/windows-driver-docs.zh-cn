---
title: Direct3D 驱动程序回调的返回代码
description: Direct3D 驱动程序回调的返回代码
keywords:
- Direct3D WDK Windows 2000 显示，返回代码
- 返回代码 WDK Direct3D
- 回调 WDK Direct3D
- 回调函数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de347295b431b473d41cc1ea7ec8f37157f54273
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812577"
---
# <a name="return-codes-for-direct3d-driver-callbacks"></a>Direct3D 驱动程序回调的返回代码

下表列出了可以由 [Direct3D Driver-Supplied 函数](driver-functions-to-support-direct3d.md)返回的值。 在 DWORD 返回值中实际返回 DDHAL_DRIVER_ *Xxx* 值。 D3D_OK 值、D3DHAL_ *Xxx* 值和 D3DERR_ *xxx* 错误代码将在特定函数的参数指向的结构的 **ddrval** 成员中返回。

有关每个函数可以返回的特定错误代码，请参阅参考部分中的函数和结构说明。 有关错误代码和返回 (值的 *完整列表，* 请参阅 Direct3D 标头文件 *d3dhal 和* ， *d3d8* 和 *d3d9* 用于 DirectX 版本8.0 和 9.0) 。 请注意，错误代码由负值表示，不能组合使用。

Direct3D 驱动程序中的函数必须返回两个返回代码之一： DDHAL_DRIVER_HANDLED 或 DDHAL_DRIVER_NOTHANDLED。 如果驱动程序返回 DDHAL_DRIVER_HANDLED，则它还必须返回 D3D_OK 或 *D3D* 或 *d3dhal* 中列出的值之一。 Direct3D 驱动程序中的函数可以返回下表中的值。 这些值在 *d3d .h* 和 *d3dhal* 中定义。

| 值 | 含义 |
| ----- | ------- |
| D3D_OK (定义为 DD_OK)  | 请求已成功完成。 |
| D3DHAL_CONTEXT_BAD | 传入的上下文无效。 |
| DDHAL_DRIVER_HANDLED | 驱动程序已执行该操作，并在传递给驱动程序的回调的结构的 **ddrval** 成员中返回了该操作的有效返回代码。 如果 D3D_OK 此代码，Direct3D 将继续执行此函数。 否则，Direct3D 将返回驱动程序提供的错误代码，并中止该函数。 |
| DDHAL_DRIVER_NOTHANDLED | 驱动程序在请求的操作上没有注释。 如果需要驱动程序实现特定的回调，Direct3D 会报告错误情况。 否则，Direct3D 会处理该操作，就像未通过执行 Direct3D 与设备无关的实现来定义驱动程序回调。 Direct3D 通常会忽略回调的参数结构的 **ddrval** 成员中返回的任何值。 |
| D3DHAL_OUTOFCONTEXTS | 此进程中没有剩余的上下文。 |
| D3DERR_UNSUPPORTEDCOLOROPERATION | 颜色操作不受支持。 |
