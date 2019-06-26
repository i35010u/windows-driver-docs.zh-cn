---
title: 显示驱动程序初始化
description: 显示驱动程序初始化
ms.assetid: a4cc7780-b6fb-486a-b54b-96c90d4fe1f5
keywords:
- 显示驱动程序 WDK Windows 2000 中，初始化
- 初始化显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d7880030e48db7c852fd8328413b1dcbb1f8866
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359357"
---
# <a name="display-driver-initialization"></a>显示驱动程序初始化


## <span id="ddk_display_driver_initialization_gg"></span><span id="DDK_DISPLAY_DRIVER_INITIALIZATION_GG"></span>


显示驱动程序初始化是类似于图形驱动程序初始化，如中所述[支持初始化和终止函数](supporting-initialization-and-termination-functions.md)。 本部分提供了特定可以显示驱动程序的初始化详细信息。

视频的微型端口和显示驱动程序初始化后加载和初始化 NT 高级管理人员和 Win32 子系统出现。 系统将加载的微型端口驱动程序或驱动程序在注册表中，启用的然后确定的微型端口驱动程序和要使用的显示驱动程序对。 在此过程中，GDI 将打开所有必要的显示驱动程序，根据窗口管理器提供的信息。

基本显示驱动程序初始化过程中，在其中桌面后下, 图中所示。

![关系图演示如何显示驱动程序初始化](images/202-01.png)

1.  当调用 GDI 以创建第一个设备上下文 (*DC*) 的视频硬件 GDI 调用显示驱动程序函数[ **DrvEnableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)。 在返回时， **DrvEnableDriver**提供了与 GDI [ **DRVENABLEDATA** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdrvenabledata)保存驱动程序的图形 DDI 的版本号和所有的入口点的结构可调用图形驱动程序实现的 DDI 函数 (而不**DrvEnableDriver**)。

2.  GDI 然后调用驱动程序的[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)函数请求驱动程序的物理设备特性的说明。 在调用中，GDI 传入[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构，它标识 GDI 想要设置的模式。 如果 GDI 请求显示或基础微型端口驱动程序不支持的模式，则显示驱动程序必须失败此调用。

3.  显示驱动程序表示控制的 GDI 逻辑设备。 下图中所示，单个逻辑设备可以管理多个物理设备，每个特征的硬件、 逻辑地址和应用层协议支持的类型。 显示驱动程序分配的内存来支持的设备创建。 显示驱动程序可能会调用来管理多个*PDEV*的同一个物理设备，尽管只有一个 PDEV 可以启用为给定的物理设备一次。 在单独创建每个 PDEV GDI 调用[ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)，并每次调用创建另一个 PDEV 用于不同的图面。

    驱动程序必须支持多个 PDEV，因为它不应使用全局变量。

    下图说明了逻辑与物理设备。

    ![说明逻辑与物理设备的关系图](images/202-03.png)

4.  物理设备的安装完成时，调用 GDI [ **DrvCompletePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)。 此函数提供了与 GDI 生成物理设备句柄来请求设备的 GDI 函数时使用的驱动程序。

5.  在初始化的最后阶段，图面创建的视频硬件通过 GDI 调用[ **DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)，这样对硬件的图形输出。 具体取决于设备和环境中，显示驱动程序，在两种方式之一面：
    -   该驱动程序通过调用 GDI 函数来管理其自己图面**EngCreateDeviceSurface**方法是所必需的硬件不支持的标准格式位图，对于硬件不是可选的。
    -   GDI 可以管理面作为完全*引擎管理面*如果硬件设备已组织成标准格式位图的表面。 驱动程序可以调用[ **EngModifySurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmodifysurface)转换*设备管理*为一个主位图*引擎管理*。 该驱动程序仍可以挂接任意绘制操作。

任何现有的 GDI 位图的句柄是有效的图面上句柄。 驱动程序可以调用[ **EngModifySurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmodifysurface)若要将设备管理主位图转换为托管引擎的位图。 如果在图面，引擎管理 GDI 可以处理任何或所有绘制操作。 如果在图面是设备管理，在最低限度，该驱动程序必须处理[ **DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)， [ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)，和[**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)。


GDI 调用后将自动启用 DirectDraw [ **DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)。 DirectDraw 初始化后，该驱动程序可以使用 DirectDraw 的*堆管理器*执行[*屏幕外内存*](video-present-network-terminology.md#off_screen_memory)管理。 请参阅[DirectDraw 和 GDI](directdraw-and-gdi.md)有关详细信息。


显示驱动程序必须实现[ **DrvNotify** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnotify)为了接收通知的事件，特别是 DN\_绘图\_开始事件。 GDI 发送该事件之前它将开始绘图，因此它可以用于确定何时可以初始化缓存。

请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)部分，了解有关启动过程的详细信息。



 





