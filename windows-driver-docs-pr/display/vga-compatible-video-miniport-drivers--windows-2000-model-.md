---
title: 兼容的 VGA 视频微型端口驱动程序 （Windows 2000 模式）
description: 兼容的 VGA 视频微型端口驱动程序 （Windows 2000 模式）
ms.assetid: c3a7bcbc-d9e9-488c-9e97-34ab85489ab9
keywords:
- 微型端口驱动程序 WDK Windows 2000 中 VGA
- VGA WDK 微型端口
- VGA WDK 视频的微型端口，有关兼容的 VGA 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29aff21d5a8b273961cc420b0db123b0c5850d1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527044"
---
# <a name="vga-compatible-video-miniport-drivers-windows-2000-model"></a>兼容的 VGA 视频微型端口驱动程序 （Windows 2000 模式）


## <span id="ddk_vga_compatible_video_miniport_drivers_windows_2000_model__gg"></span><span id="DDK_VGA_COMPATIBLE_VIDEO_MINIPORT_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


在基于 x86 的基于 NT 的操作系统平台上有两种类型的微型端口驱动程序： nonVGA 兼容微型端口驱动程序和兼容的 VGA 的微型端口驱动程序。

大多数微型端口驱动程序 nonVGA 兼容，因此更易于实现。 NonVGA 兼容微型端口驱动程序依赖于具有系统提供的 VGA 微型端口驱动程序 (vga.sys) 或另一个兼容的 VGA SVGA 微型端口同时加载驱动程序。 这样的微型端口驱动程序设置来配置本身在注册表中与 VgaCompatible 设置为零 (FALSE)，并具有以下功能：

-   它不提供特殊支持基于 x86 的计算机中的全屏幕 MS-DOS 应用程序。 相反，它加载以及系统提供的 VGA （或者，也可能使用 VGA 兼容的 SVGA） 微型端口驱动程序，全屏幕 MS-DOS 应用程序提供此支持。

-   在大多数情况下，它也是编写了没有 VGA 兼容性模式的适配器或加速器，独立于 VGA。

兼容的 VGA 的微型端口驱动程序为基础的系统提供的 VGA 微型端口驱动程序，使用代码修改，以支持特定于适配器的功能。 系统提供的 VGA 显示器驱动程序使用提供兼容的 VGA 的微型端口驱动程序，这样的新兼容的 VGA 的适配器的微型端口驱动程序开发人员不需要编写新的显示器驱动程序的支持。 它提供的全屏 MS-DOS 应用程序可以直接向适配器寄存器 I/O 的支持。 它还用作视频的验证程序，以防止此类应用程序发出任何序列将挂起计算机的说明。

自声明"兼容的 VGA"微型端口驱动程序设置为在注册表中自行配置使用 VgaCompatible 设置为 1 (TRUE)。

在基于 x86 的计算机兼容的 VGA 的微型端口驱动程序将为系统提供的 VGA 微型端口驱动程序。 因此，兼容的 VGA 的微型端口驱动程序必须具有一套*SvgaHwIoPortXxx*函数来支持全屏幕 MS-DOS 应用程序，如系统提供的 VGA 微型端口驱动程序执行。

新的 VGA 兼容的 SVGA 微型端口驱动程序的设计器都应灵活掌握系统提供 SVGA 微型端口驱动程序之一*SvgaHwIoPortXxx*函数适配器的功能。 对于其他类型的基于 x86 的计算机中的适配器的微型端口驱动程序可以有一套*SvgaHwIoPortXxx*例程，并提供相同裁量权微型端口驱动程序设计器的支持或如果不能加载微型端口驱动程序虽然加载系统 VGA 微型端口驱动程序。

 

 





