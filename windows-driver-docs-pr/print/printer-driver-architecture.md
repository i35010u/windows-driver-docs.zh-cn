---
title: 打印机驱动程序体系结构
description: 打印机驱动程序体系结构
ms.assetid: 68a61007-8f0d-4fd4-b4a7-c8acbc101236
keywords:
- 打印作业 WDK，打印机驱动程序
- 作业 WDK 打印，打印机驱动程序
- Windows 打印体系结构 WDK
- 打印机驱动程序体系结构 WDK
- 打印机驱动程序 WDK，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52b37c265d82161419c2c07293a7fbc83aa396d3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216346"
---
# <a name="printer-driver-architecture"></a>打印机驱动程序体系结构





打印作业由应用程序通过调用 Microsoft Win32 GDI 或在 Windows Vista 中 Windows Presentation Foundation (WPF) 函数创建。 Win32 函数以 EMF 形式处理应用程序数据，或者它们可以立即呈现每个文档页的可打印图像。 WPF 以 XPS 假脱机文件的形式处理应用程序数据。

在 Windows Vista 之前，应用程序使用 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构将打印机设置传达给打印机。 在 Windows Vista 中，打印票证和打印功能技术将打印机设置进行通信，以便在打印机和应用程序之间更兼容打印机设置。

图像呈现，无论是立即执行还是在打印处理过程中，都在打印驱动程序中执行：

-   [基于 gdi 的打印机驱动程序](gdi-printer-drivers.md)在从假脱机文件中播放 EMF 记录时执行图像呈现，由 GDI 呈现引擎控制。 在呈现操作期间，GDI 呈现引擎将调用相应的 Windows 2000 和更高版本的打印机驱动程序以获得帮助。

-   [XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md) 使用一系列处理筛选器来处理 XPS 假脱机文件内容，以便输出到打印机。

Windows 2000 和更高版本的基于 GDI 的打印机驱动程序必须：

-   通过提供 GDI 无法支持的特定于打印机的绘图功能，帮助 GDI 呈现打印作业。

-   将呈现的图像的数据流发送到打印后台处理程序。

-   提供与打印机和打印文档关联的可修改配置参数的用户界面，如选择的输入和输出送纸器、副本的数量、图像分辨率和方向等。

XPSDrv 打印机驱动程序与基于 GDI 的驱动程序具有相同的用户界面责任，还负责处理打印作业数据并将数据发送到打印机。 但 XPSDrv 打印机驱动程序无需使用 GDI 来呈现打印机的页面图像。

Windows 2000 和更高版本的打印机驱动程序由一组 [打印机驱动程序组件](gdi-printer-drivers.md) 组成，这些组件将驱动程序的绘图和用户界面操作划分为单独的 dll。 XPSDrv 打印机驱动程序也由组件组成，这些组件将配置和绘制和呈现功能分为单独的对象。

本部分旨在帮助你了解 Windows 2000 和更高版本操作系统支持的不同类型的打印机驱动程序，但你还应记住，操作系统附带了以下三个打印机驱动程序：

[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)

[Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md)

[Microsoft 绘图仪驱动程序](microsoft-plotter-driver.md)

这三个驱动程序支持最终用户可以立即购买的大多数打印设备。 仅当打印设备与相应的 Microsoft 提供的驱动程序不兼容时，才需要编写打印机驱动程序。 只需将 [打印机数据文件](printer-data-files.md) 添加到 Microsoft 提供的某个驱动程序，即可支持大多数新打印机。 可能需要新驱动程序的设备包括包含由专有命令序列控制的硬件绘图加速器的设备。

本部分包含以下主题，其中介绍了 Windows 打印体系结构。

[XPSDrv 打印机驱动程序](xpsdrv-printer-drivers.md)

[GDI 打印机驱动程序](gdi-printer-drivers.md)

[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)

[编写 64 位打印机驱动程序](writing-64-bit-printer-drivers.md)

 

