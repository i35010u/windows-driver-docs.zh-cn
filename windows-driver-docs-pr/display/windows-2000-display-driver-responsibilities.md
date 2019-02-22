---
title: Windows 2000 显示驱动程序责任
description: Windows 2000 显示驱动程序责任
ms.assetid: ccd7ff38-a4a3-4917-bf59-c2a1b864d026
keywords:
- 显示器驱动程序模型 WDK Windows 2000，职责
- Windows 2000 显示器驱动程序模型 WDK，职责
- 显示驱动程序 WDK Windows 2000 中，有关显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4f6d8315573030aad84cc541a915f0812b19f4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545509"
---
# <a name="windows-2000-display-driver-responsibilities"></a>Windows 2000 显示驱动程序责任


## <span id="ddk_display_driver_responsibilities_gg"></span><span id="DDK_DISPLAY_DRIVER_RESPONSIBILITIES_GG"></span>


一个*显示器驱动程序*是为其主要职责是一个内核模式 DLL*呈现*。 当应用程序调用与设备无关的图形请求的 Win32 函数时，图形设备接口 (GDI) 解释这些说明，并调用显示器驱动程序。 显示器驱动程序，然后将这些请求转换为用于在屏幕上绘制图形的视频硬件的命令。

显示驱动程序可以直接访问硬件。 这是因为图形硬件功能，在各种不同并且显示是任何系统的时间最关键部分之一。 此可访问性和宽于 GDI 中的功能的作用域时实现显示器驱动程序提供相当大的灵活性。

-   默认情况下，GDI 绘制操作处理上*标准格式的位图*，此类包括的硬件上一样*帧缓冲区*。 显示驱动程序可以挂接和实现的任何[的绘图功能](optional-display-driver-functions.md)为硬件提供特殊支持。 对于较少的时间关键操作和图形适配器不支持更复杂的操作，该驱动程序可以回 GDI 被迫函数并允许 GDI 执行工作。 请参阅[挂接 Versus Punting](hooking-versus-punting.md)有关详细信息。

-   尤其是时间关键操作显示驱动程序可以直接访问视频硬件寄存器。 例如，VGA 显示器的驱动程序*x*86 系统使用优化的程序集代码以实现一些绘图和文本操作直接访问硬件寄存器。
    **请注意**  微型端口驱动程序必须管理的微型端口驱动程序和显示驱动程序之间共享的所有资源 （例如，内存资源）。 系统不保证始终将微型端口驱动程序可以访问在显示器驱动程序中获取的资源。

     

中详细介绍了显示器驱动程序[显示驱动程序 （Windows 2000 模式）](display-drivers--windows-2000-model-.md)。

 

 





