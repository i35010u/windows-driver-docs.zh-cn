---
title: Windows 2000 显示驱动程序的责任
description: Windows 2000 显示驱动程序的责任
keywords:
- 显示驱动程序模型 WDK Windows 2000，责任
- Windows 2000 显示器驱动程序模型 WDK，责任
- 显示驱动程序 WDK Windows 2000，关于显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f88bd5da73b2dc7678b304ce5872cf8107c1367e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826011"
---
# <a name="windows-2000-display-driver-responsibilities"></a>Windows 2000 显示驱动程序的责任


## <span id="ddk_display_driver_responsibilities_gg"></span><span id="DDK_DISPLAY_DRIVER_RESPONSIBILITIES_GG"></span>


*显示驱动程序* 是一种内核模式 DLL，主要责任在此 DLL 中 *呈现*。 当应用程序使用与设备无关的图形请求调用 Win32 函数时，图形设备接口 (GDI) 会解释这些指令并调用显示驱动程序。 然后，显示驱动程序将这些请求转换为视频硬件的命令，以在屏幕上绘制图形。

显示驱动程序可以直接访问硬件。 这是因为图形硬件功能有很大的不同，因此显示是任何系统中最重要的部分。 在实现显示驱动程序时，GDI 中的这种可访问性和各种功能范围提供了相当大的灵活性。

-   默认情况下，GDI 处理 *标准格式位图* 的绘图操作，例如在包含 *帧缓冲区* 的硬件上。 显示驱动程序可以挂钩并实现硬件提供特殊支持的任何 [绘图函数](optional-display-driver-functions.md) 。 对于更少的时间关键操作和图形适配器不支持的复杂操作，驱动程序可以将函数改回 GDI 并允许 GDI 完成工作。 有关详细信息，请参阅 [挂钩与 Punting](hooking-versus-punting.md) 。

-   对于特别时间关键的操作，显示驱动程序可以直接访问视频硬件寄存器。 例如，适用于 *x* 86 系统的 VGA 显示器驱动程序使用优化的程序集代码来实现对某些绘图和文本操作的硬件寄存器的直接访问。
    **注意**   视频微型端口驱动程序必须管理所有资源， (例如，视频微型端口驱动程序与显示驱动程序之间共享) 内存资源。 系统不保证显示驱动程序中获取的资源始终可由视频微型端口驱动程序访问。

     

显示驱动程序在 [ (Windows 2000 模型) 的 "显示驱动程序 ](display-drivers--windows-2000-model-.md)" 中详细讨论。

 

 





