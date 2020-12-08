---
title: VGA 兼容的视频微型端口驱动程序（Windows 2000 模型）
description: VGA 兼容的视频微型端口驱动程序（Windows 2000 模型）
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、VGA
- VGA WDK 视频微型端口
- VGA WDK 视频微型端口，关于 VGA 兼容驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf8e6ef2051fbbcfa75ee85aea052d7ad6e5a1cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823275"
---
# <a name="vga-compatible-video-miniport-drivers-windows-2000-model"></a>VGA 兼容的视频微型端口驱动程序（Windows 2000 模型）


## <span id="ddk_vga_compatible_video_miniport_drivers_windows_2000_model__gg"></span><span id="DDK_VGA_COMPATIBLE_VIDEO_MINIPORT_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


在基于 x86 的基于 NT 的操作系统平台上，有两种类型的视频微型端口驱动程序： nonVGA 兼容的微型端口驱动程序和与 VGA 兼容的微型端口驱动程序。

大多数微型端口驱动程序都是 nonVGA 兼容的，因此实现起来要简单得多。 NonVGA 兼容的视频微型端口驱动程序依赖于让系统提供的 VGA 微型端口驱动程序 ( # A0) 或同时加载的其他 VGA 兼容 SVGA 微型端口驱动程序。 此类微型端口驱动程序设置为在注册表中配置自身，将 VgaCompatible 设置为零 (FALSE) 并且具有以下功能：

-   它不提供对基于 x86 的计算机中全屏 MS-DOS 应用程序的特殊支持。 相反，它是与系统提供的 VGA (一起加载的，也可能是使用与 VGA 兼容的 SVGA) 微型端口驱动程序提供的，它为全屏 MS-DOS 应用程序提供此支持。

-   在大多数情况下，它是针对没有 VGA 兼容模式的适配器或针对独立于 VGA 的加速器编写的。

VGA 兼容的微型端口驱动程序基于系统提供的 VGA 微型端口驱动程序，并且修改了代码以支持特定于适配器的功能。 系统提供的 VGA 显示驱动程序使用由 VGA 兼容的微型端口驱动程序提供的支持，因此用于 VGA 兼容适配器的新微型端口驱动程序的开发人员无需编写新的显示驱动程序。 它支持全屏 MS-DOS 应用程序直接对适配器注册执行 i/o 操作。 它还充当视频验证程序，以防止此类应用程序发出会挂起计算机的任何指令序列。

自声明的 "VGA 兼容" 微型端口驱动程序设置为在注册表中配置自身，并将 VgaCompatible 设置为一 (TRUE) 。

基于 x86 的计算机中的 VGA 兼容小型端口驱动程序替换系统提供的 VGA 微型端口驱动程序。 因此，与系统提供的 VGA 微型端口驱动程序一样，与 VGA 兼容的微型端口驱动程序必须具有一组 *SvgaHwIoPortXxx* 函数来支持全屏 MS-DOS 应用程序。

新的 VGA 兼容 SVGA 微型端口驱动程序的设计器应将系统提供的 SVGA 微型端口驱动程序的 *SvgaHwIoPortXxx* 函数调整为适配器的功能。 基于 x86 的计算机中其他类型的适配器的微型端口驱动程序可以具有一组 *SvgaHwIoPortXxx* 例程，并按微型端口驱动程序设计器的判断提供相同的支持，或者，如果在加载系统 VGA 微型端口驱动程序时无法加载微型端口驱动程序。

 

 





