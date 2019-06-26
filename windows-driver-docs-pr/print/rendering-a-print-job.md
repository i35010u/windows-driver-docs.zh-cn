---
title: 渲染打印作业
description: 渲染打印作业
ms.assetid: 78967839-b518-41c0-8825-b00f8b8560e6
keywords:
- 打印机图形 DLL WDK，呈现打印作业
- 图形 DLL WDK 打印机，呈现打印作业
- 呈现打印作业 WDK
- 打印作业 WDK 呈现
- WDK 的打印作业呈现
- 具有带区 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 909275ada9c8ccd101b8a503d140d9cb2bde850b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383532"
---
# <a name="rendering-a-print-job"></a>渲染打印作业





在创建或作为 EMF 记录写入到假脱机文件时可以呈现打印作业。 在 EMF 记录的情况下呈现采用当 EMF*打印处理器*(localspl.dll) 播放记录。 呈现的调用的用户模式下 GDI 绘图功能，从一系列组成**CreateDC** （Microsoft Windows SDK 文档中所述）。 在调用**CreateDC**是一系列应用程序调用会导致的操作涉及图形呈现引擎 (GRE，也称为内核模式 GDI) 和打印机图形 DLL 链中的第一个。

下图显示了内核模式 GDI 和打印机图形 DLL 之间的交互后**CreateDC**调用。

![在调用 createdc 后说明内核模式 gdi 和打印机图形 dll 之间的交互的关系图](images/gdirendr2.png)

1.  当应用程序调用**CreateDC**创建打印机设备上下文，GDI 函数检查是否加载相应的打印机图形 DLL。 如果不是，将加载的 DLL 和调用 GDI [ **DrvEnableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver) DLL 中的函数。 除非重新加载该驱动程序，不是再次调用的函数。

2.  接下来，GDI 调用打印机图形 DLL 的[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)函数，该驱动程序可以创建一个物理设备实例并返回设备特征。 GDI 使用返回的信息来创建设备实例的内部说明。

3.  GDI 然后调用图形 DLL 的[ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)函数提供的 GDI 句柄设备实例。 图形 DLL 必须使用此句柄作为输入的一些**Eng**-前缀 GDI 绘图引擎提供的回调 (请参阅[GDI 支持服务](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-support-services))。

4.  GDI 收到设备实例句柄后，因此，可以通过图形 DLL 的调用[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)函数，它将设置进行绘制，图面，将其与物理设备关联实例。

5.  该驱动程序可以通过调用创建的设备实例绘图图面[ **EngCreateBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)。 或者，如果绘图图面是设备管理，该驱动程序可以调用[ **EngCreateDeviceSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)。

6.  如果**EngCreateBitmap**不能提供足够大以包含整个物理页的位图，如果该驱动程序支持页条带， [ **EngMarkBandingSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface)可以是调用以通知 GDI 将采用条带。

7.  最后， [ **EngAssociateSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface)必须调用以允许使用指定的设备实例，将创建的图面并使能够知道哪些驱动程序所提供的图形 DDI 绘图的 GDI GDI函数 （如果有） 则应调用此特定的图面上绘制时。

此时，已创建绘图图面，可以开始呈现。 条带是否有效取决于 GDI 调用的函数。

### <a name="banding-in-use"></a>在使用条带

对于每个文档以进行呈现时使用条带，GDI 打印机图形 DLL 中调用以下函数：

[**DrvStartDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)为每个物理页 { [ **DrvStartPage**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)
[**DrvStartBanding** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartbanding)为一个物理页上的每个联合阶段 { [ *DrvQueryPerBandInfo* ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)呈现操作[ **DrvNextBand** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)发送此区段的光栅数据然后清除面以重复用于下一步外}} [ **DrvEndDoc**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)
### <a href="" id="banding-not-in-use"></a> 在不使用条带

对于每个文档以进行呈现时不使用条带，GDI 打印机图形 DLL 中调用以下函数：

[**DrvStartDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc)为每个物理页面[ **DrvStartPage** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartpage)呈现操作[ *DrvSendPage* ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage)/ / 发送页的光栅数据} [ **DrvEndDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)除[ *DrvQueryPerBandInfo*](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryperbandinfo)，则这些函数为了让其打印机图形 DLL 将发送到打印机硬件的控制序列 (通过调用[ **EngWritePrinter**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter))，并执行任何所需的内部操作若要初始化或已完成的文档、 页或带内处理。

打印机图形 DLL 负责在适当的时候将呈现的图像 （即，内容的绘图图面） 发送到打印机 (通过调用**EngWritePrinter**)，按如下所示：

-   对于 GDI 管理或由设备管理位图图面

    绘图图面是 GDI 提供或者驱动程序提供的位图。 打印机图形 DLL 可能挂钩一些绘图函数 (请参阅[面协商](https://docs.microsoft.com/windows-hardware/drivers/display/surface-negotiation))。 如果页条带正在使用中， [ **DrvNextBand** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnextband)函数应发送绘制图面上的内容。 如果在使用中，条带不是[ *DrvSendPage* ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsendpage)函数应发送绘图图面上的内容。

-   对于设备管理矢量图面

    在设备中的绘图图面。 打印机图形 DLL 挂钩所有绘图函数 (请参阅[面协商](https://docs.microsoft.com/windows-hardware/drivers/display/surface-negotiation))，并且这些函数在呈现操作期间将映像数据发送到打印机。 不使用条带的页。

如果希望在任何图形 DDI 函数提供由打印机图形 DLL 起来可能需要超过五秒的时间来执行，则应包含调用的代码[ **EngCheckAbort** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcheckabort)至少若要了解是否应终止打印作业每隔 5 秒。

在 GDI 后调用[ **DrvEndDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenddoc)若要指示已完全呈现文档，它会调用[ **DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)。 如果[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)调用[ **EngCreateBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)，然后**DrvDisableSurface**必须调用[ **EngDeleteSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesurface)。

GDI 调用打印机图形 DLL 的[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)函数，当应用程序调用**DeleteDC**。

如果应用程序调用**ResetDC**函数在一个文档，GDI 打印过程中的创建新的设备上下文，调用打印机图形 DLL 的[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)新的上下文的函数。 然后调用 GDI [ **DrvResetPDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)函数，使图形 DLL 可以使用来自旧信息更新新的上下文。 下一步， [ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)并[ **DrvDisablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)调用旧的上下文中后, 跟[ **DrvEnableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)新上下文。 最后，调用 GDI [ **DrvStartDoc** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstartdoc) ，呈现继续在新页。

GDI 调用[ **DrvDisableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)之前卸载打印机图形 DLL。

如果打印机硬件支持 GDI 绘图函数不支持的绘图操作，打印机图形 DLL 可以提供[ **DrvDrawEscape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)函数。

DLL 可以提供的打印机图形[ **DrvEscape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)函数是否需要以支持绘制或非绘图操作所不具备通过 GDI 函数。 例如， [Microsoft PostScript 的打印机驱动程序](microsoft-postscript-printer-driver.md)使用转义符来支持 PostScript 注入点。 或者，应用程序可能需要获取传真机的电话号码。 **DrvEscape**函数还可用于支持的操作，该值指示**DrvDrawEscape**函数。

**CreateDC**， **ResetDC**，和**DeleteDC** Microsoft Windows SDK 文档中所述。

 

 




