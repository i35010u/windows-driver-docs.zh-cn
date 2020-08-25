---
title: 渲染打印作业
description: 渲染打印作业
ms.assetid: 78967839-b518-41c0-8825-b00f8b8560e6
keywords:
- 打印机图形 DLL WDK，呈现打印作业
- 图形 DLL WDK 打印机，呈现打印作业
- 呈现打印作业 WDK
- 作业 WDK 打印，渲染
- 打印作业 WDK，呈现
- 分级 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 555903c1a3c0fb7e2c48cb3a505e34730c982a14
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802425"
---
# <a name="rendering-a-print-job"></a>渲染打印作业





打印作业在创建时呈现，或者作为 EMF 记录写入到假脱机文件中。 对于 EMF 记录，在 EMF *打印处理器* ( # A0) 播放记录时进行呈现。 呈现由一系列对用户模式 GDI 绘图函数的调用（从 "Microsoft Windows SDK 文档) " 中所述的 **CreateDC** (开始）组成。 对 **CreateDC** 的调用是一系列应用程序调用中的第一个，它们会导致一系列涉及图形呈现 (引擎的操作，这些操作又称为内核模式 GDI) 和打印机图形 DLL。

下图显示了 **CreateDC** 调用后内核模式 GDI 和打印机图形 DLL 之间的交互。

![说明调用 createdc 后内核模式 gdi 和打印机图形 dll 之间的交互的关系图](images/gdirendr2.png)

1.  当应用程序调用 **CreateDC** 函数来创建打印机设备上下文时，GDI 将检查是否已加载适当的打印机图形 DLL。 如果不是，则 GDI 将加载 DLL 并调用 DLL 中的 [**DrvEnableDriver**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenabledriver) 函数。 除非重新加载了驱动程序，否则不会再次调用该函数。

2.  接下来，GDI 将调用打印机图形 DLL 的 [**DrvEnablePDEV**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数，以便驱动程序可以创建物理设备实例并返回设备特征。 GDI 使用返回的信息创建设备实例的内部说明。

3.  然后，GDI 将调用图形 DLL 的 [**DrvCompletePDEV**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvcompletepdev) 函数，以向设备实例提供 GDI 句柄。 图形 DLL 必须使用此句柄来输入 GDI 绘图引擎提供的一些以 **Eng**为前缀的回调 (请参阅 [gdi 支持服务](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-support-services)) 。

4.  在 GDI 接收到设备实例句柄之后，它将调用图形 DLL 的 [**DrvEnableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数，该函数会为绘图设置图面，并将其与物理设备实例相关联。

5.  驱动程序可以通过调用 [**EngCreateBitmap**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engcreatebitmap)为设备实例创建绘图图面。 或者，如果绘图图面是设备托管的，则驱动程序可以调用 [**EngCreateDeviceSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engcreatedevicesurface)。

6.  如果 **EngCreateBitmap** 无法提供足够大的位图来包含整个物理页面，并且如果驱动程序支持页面条带，则可以调用 [**ENGMARKBANDINGSURFACE**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engmarkbandingsurface) 来通知 GDI 将使用条带。

7.  最后，必须调用 [**EngAssociateSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engassociatesurface) ，以允许 gdi 将创建的表面与指定的设备实例相关联，并让 gdi 知道哪个驱动程序提供的图形 DDI 绘图函数 (在它绘制到此特定图面上时应调用的任何) 。

此时，已创建了一个绘图图面，可以开始渲染。 GDI 调用的函数取决于分级是否有效。

### <a name="banding-in-use"></a>使用中的条带

对于在使用条带时要呈现的每个文档，GDI 将调用打印机图形 DLL 中的以下函数：

[**DrvStartDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc)对于每个物理页[**{DrvStartPage**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartpage) 
 [**DrvStartBanding**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartbanding) for a for a for a [*DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo)呈示操作[**DrvNextBand**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvnextband) //发送此波段的光栅数据，然后清除 "要重新使用下一带区的图面}" [**DrvEndDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenddoc)
### <a name="banding-not-in-use"></a><a href="" id="banding-not-in-use"></a> 未使用分级

对于在未使用条带时要呈现的每个文档，GDI 将调用打印机图形 DLL 中的以下函数：

[**DrvStartDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc) 对于每个物理页 [**DrvStartPage**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartpage) 呈现操作 [*DrvSendPage*](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsendpage) //发送页面的光栅数据} [**DrvEndDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenddoc) ，但 [*DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryperbandinfo)除外，这些函数旨在允许打印机图形 DLL 通过调用 [**EngWritePrinter**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engwriteprinter)) 将控制序列发送到打印机硬件 (，以及执行初始化或完成文档、页面或带区的任何内部操作。

打印机图形 DLL 负责发送呈现的图像 (即，绘图图面的内容在适当时间通过调用 **EngWritePrinter**) ) 到打印机 (，如下所示：

-   对于 GDI 托管或设备托管的位图图面

    绘图图面是 GDI 提供的或驱动程序提供的位图。 打印机图形 DLL 可能会挂钩某些绘图功能 (请参阅 [Surface 协商](https://docs.microsoft.com/windows-hardware/drivers/display/surface-negotiation)) 。 如果正在使用页面色带，则 [**DrvNextBand**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvnextband) 函数应发送绘图图面内容。 如果未使用条带，则 [*DrvSendPage*](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvsendpage) 函数应发送绘图图面内容。

-   对于设备托管的矢量图面

    绘图图面在设备内。 打印机图形 DLL 挂钩所有绘图功能 (请参阅 [Surface 协商](https://docs.microsoft.com/windows-hardware/drivers/display/surface-negotiation)) ，这些函数在呈现操作过程中将图像数据发送到打印机。 不使用页面条。

如果预计打印机图形 DLL 提供的任何图形 DDI 函数可能需要超过5秒的执行时间，则应包括至少每五秒调用 [**EngCheckAbort**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engcheckabort) 的代码，以查看打印作业是否应终止。

在调用 [**DrvEndDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenddoc) 以指示文档完全呈现后，它将调用 [**DrvDisableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablesurface)。 如果 [**DrvEnableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface) 名为 [**EngCreateBitmap**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engcreatebitmap)，则 **DrvDisableSurface** 必须调用 [**EngDeleteSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-engdeletesurface)。

当应用程序调用**DeleteDC**时，GDI 将调用打印机图形 DLL 的[**DrvDisablePDEV**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablepdev)函数。

如果应用程序在打印文档的过程中调用 **ResetDC** 函数，则 GDI 会创建一个新的设备上下文，并为新上下文调用打印机图形 DLL 的 [**DrvEnablePDEV**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数。 GDI 将调用 [**DrvResetPDEV**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvresetpdev) 函数，因此，图形 DLL 可以用旧的信息更新新的上下文。 接下来，为旧上下文调用 [**DrvDisableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablesurface) 和 [**DrvDisablePDEV**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisablepdev) ，后跟新上下文的 [**DrvEnableSurface**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvenablesurface) 。 最后，在新页上，GDI 将调用 [**DrvStartDoc**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvstartdoc) 并呈现恢复。

在卸载打印机图形 DLL 之前，GDI 将调用 [**DrvDisableDriver**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdisabledriver) 。

如果打印机硬件支持 GDI 绘图函数不支持的绘图操作，则打印机图形 DLL 可提供 [**DrvDrawEscape**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvdrawescape) 函数。

如果需要支持无法通过 GDI 函数使用的绘图或 nondrawing 操作，打印机图形 DLL 可以提供 [**DrvEscape**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvescape) 函数。 例如， [Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md) 使用转义以支持 PostScript 注入点。 或者，应用程序可能需要获取传真计算机的电话号码。 **DrvEscape**函数还用于指示**DrvDrawEscape**函数支持的操作。

Microsoft Windows SDK 文档中介绍了**CreateDC**、 **ResetDC**和**DeleteDC** 。

 

 




