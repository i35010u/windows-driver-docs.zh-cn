---
title: 高保真打印输出
description: 高保真打印输出
keywords:
- 颜色保真 WDK XPSDrv
- 打印保真度 WDK XPSDrv
- 高保真打印输出 WDK XPSDrv
- XPSDrv 打印机驱动程序 WDK，高保真打印输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd2a56d5ba7f14a38d7668aeed1a3f6500beab80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796857"
---
# <a name="high-fidelity-print-output"></a>高保真打印输出


基于 XPS 的打印机可以提供整体改进的打印和色彩保真度。 当最终用户从 Windows Presentation Foundation () WPF 上构建的应用程序打印或将输出定向到基于 XPS 的打印机或驱动程序时，XPS 打印路径会尽可能减少或消除图像数据转换和颜色空间转换，因此，打印输出可以保留其原始保真度。

XPS 打印为图形特性（如渐变和透明度）提供了更多的忠实渲染功能，尽管这些属性以 XPS 假脱机文件格式提供本机支持。 XPS 文档格式的 XAML 与 WPF XAML 兼容。 当用户从 WPF 应用程序打印时，Windows 操作系统将删除动画并将视频和三维 (3-d) 元素转换为图像。 所有其他图形数据都用兼容的图形基元表示，适用于设备使用。 设备或驱动程序直接使用 WPF 输出的打印版本。

在将基于 Microsoft Win32 的应用程序的输出转换为基于 XPS 的设备和驱动程序的过程中，通过对用于通过 GDI + 和渐变进行透明度模拟 (ROPs) 的特定 GDI 光栅操作进行优化，来增强打印保真度。 如果应用程序生成位图而不是使用 ROPs，则无法执行此优化。

还改进了打印到非 XPS 打印机的 WPF 应用程序的打印保真度，因为在任何应用程序都使用的 XPS 到 GDI 转换路径优于 GDI + 中的类似实现。 在不使用 GDI 光栅操作和 PostScript 位屏蔽的情况下，XPS 到 GDI 转换路径尝试 algebraically 删除透明度 (即，颜色和图像中的 alpha 通道，以及画布上画布) 的不透明度和不透明度掩码。

 

 




