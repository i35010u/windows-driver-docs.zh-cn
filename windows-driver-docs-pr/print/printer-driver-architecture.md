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
ms.openlocfilehash: 4c41685a855f42fc453c71ef300fb6c0ab9259a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525105"
---
# <a name="printer-driver-architecture"></a>打印机驱动程序体系结构





通过 Microsoft Win32 GDI，或在 Windows Vista 中，Windows Presentation Foundation (WPF) 函数的调用由应用程序会创建打印作业。 Win32 函数后台处理应用程序数据作为 EMF，或它们可以立即呈现每个文档页面的可打印图像。 WPF 的函数为 XPS 假脱机文件后台处理应用程序数据。

在 Windows Vista 之前的应用程序传递到打印机的打印机设置通过使用[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构。 Windows Vista 中的打印票证和打印功能技术通信打印机设置，以便在打印机和应用程序的打印机设置都是更加兼容。

图像呈现是否执行立即或在打印处理期间在执行打印驱动程序：

-   一个[基于 GDI 的打印机驱动程序](gdi-printer-drivers.md)图像呈现的 EMF 记录播放时执行从假脱机文件，并受 GDI 呈现引擎。 在呈现操作时，GDI 呈现引擎以获得帮助调用相应的 Windows 2000 和更高版本的打印机驱动程序。

-   [XPSDrv 打印驱动程序](xpsdrv-printer-drivers.md)使用一系列处理筛选器来处理输出到打印机的 XPS 假脱机文件内容。

Windows 2000 和更高版本基于 GDI 的打印机驱动程序必须：

-   帮助提供特定于打印机的绘图功能，以支持 GDI 不能通过 GDI 呈现打印作业。

-   将呈现的图像数据流发送到打印后台处理程序。

-   提供与打印机和打印文档，作为其输入和输出选择送纸器，如副本、 图像分辨率和方向，数和其他操作的可修改的配置参数的用户界面。

XPSDrv 的打印机驱动程序相同的用户界面负责为基于 GDI 的驱动程序，也要负责处理打印作业数据和将数据发送到打印机。 XPSDrv 的打印机驱动程序，但是，不需要使用 GDI 呈现为打印机的页面映像。

Windows 2000 和更高版本的打印机驱动程序组成的一套[打印机驱动程序组件](gdi-printer-drivers.md)，可将划分到单独的 Dll 的驱动程序的绘图和用户界面的操作。 XPSDrv 的打印机驱动程序还组成划分的配置和绘制和呈现为单独的对象的函数的组件。

本部分旨在帮助你了解不同类型的打印机驱动程序的 Windows 2000 和更高版本操作系统支持，但还应记住以下三个打印机驱动程序都附带有操作系统：

[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)

[Microsoft PostScript Printer Driver](microsoft-postscript-printer-driver.md)

[Microsoft Plotter Driver](microsoft-plotter-driver.md)

以下三个的驱动程序支持大多数最终用户可以立即购买的打印设备。 您需要编写的打印机驱动程序仅打印设备是否不与相应的 Microsoft 提供的驱动程序兼容。 您可以通过只需添加支持大多数新打印机[打印机数据文件](printer-data-files.md)到一个 Microsoft 提供的驱动程序。 可能需要新的驱动程序的设备包括这些控制的专有命令序列的包含硬件绘制加速器。

本部分包含以下主题，描述 Windows 打印体系结构。

[XPSDrv 的打印机驱动程序](xpsdrv-printer-drivers.md)

[GDI 打印机驱动程序](gdi-printer-drivers.md)

[打印票证和打印功能技术](print-ticket-and-print-capabilities-technologies.md)

[编写 64 位打印机驱动程序](writing-64-bit-printer-drivers.md)

 

 




