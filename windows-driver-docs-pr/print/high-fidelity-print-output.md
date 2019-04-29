---
title: 高保真打印输出
description: 高保真打印输出
ms.assetid: 37ff186e-d078-40f4-b7dc-9bf75e0b2847
keywords:
- 色彩保真度 WDK XPSDrv
- 打印保真度 WDK XPSDrv
- 高保真打印输出 WDK XPSDrv
- XPSDrv 的打印机驱动程序 WDK、 高保真的打印输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d304940921850603c4ed84ef85b5f78ce0e535a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360527"
---
# <a name="high-fidelity-print-output"></a>高保真打印输出


整体改进了的打印和色彩保真度，可以提供基于 XPS 的打印机。 当最终用户从基于 Windows Presentation Foundation (WPF) 还是直接输出到基于 XPS 的打印机或驱动程序的应用程序打印时，XPS 打印路径可减小或消除图像数据转换和颜色空间转换，只要有可能，因此打印输出可以保留其原始的保真度。

XPS 打印功能提供了更加忠实呈现的图形属性，如渐变样式和透明度尽管 XPS 中的这些属性的本机支持假脱机文件格式。 XAML 中的 XPS 文档格式适用于 WPF XAML。 当用户打印来自 WPF 应用程序时，Windows 操作系统中移除动画并将转换视频和三维 (3-D) 元素到映像。 适用于设备消耗的兼容的图形基元，以表示所有其他图形数据。 设备或驱动程序直接使用打印版本的 WPF 输出。

从 Microsoft 基于 Win32 的应用程序到基于 XPS 的设备和驱动程序输出自动转换，过程打印保真度增强通过优化对特定 GDI 光栅操作 (ROPs) 用于透明度模拟通过 GDI + 和渐变。 如果应用程序生成而不是使用 ROPs 位图，无法执行此优化。

从 WPF 应用程序的打印到非基于 XPS 的打印机的打印保真度也得到改进，因为 XPS GDI 转换路径优于在 GDI + 中的任何应用程序使用类似实现。 XPS GDI 转换路径尝试代数删除透明度 （即，颜色和图像和不透明度和画布上的不透明蒙板中使用 alpha 通道） 在 WPF 图形中尽可能多地，而无需使用 GDI 光栅操作和后脚本的位屏蔽。

 

 




