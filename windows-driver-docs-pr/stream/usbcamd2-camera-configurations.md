---
title: USBCAMD2 相机配置
description: USBCAMD2 相机配置
ms.assetid: 9a0dd6f9-aefb-4134-8bd5-31420a16db4a
keywords:
- Windows 2000 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- 流式处理模型 WDK Windows 2000 内核，USBCAMD2 微型驱动程序库
- 内核流式处理模型 WDK，USBCAMD2 微型驱动程序库
- USBCAMD2 照相机配置 WDK Windows 2000 内核流式处理
- 基于 USB 的流式处理相机 WDK USBCAMD2
- 照相机 WDK USBCAMD2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e050ac3c67db708feff3c1ba0983026644d9449a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373057"
---
# <a name="usbcamd2-camera-configurations"></a>USBCAMD2 相机配置


微型驱动程序以支持 USB 摄像机可能的客户端*stream.sys*其上限和他们一端较低，如以下关系图中所示的 USB 总线驱动程序上的类驱动程序。

![说明 usb 摄像机微型驱动程序模型的关系图](images/usbimdev.png)

在组中**A**关系图的配置，微型驱动程序编写器必须为接口*stream.sys*类驱动程序、 相机和 USB 总线。 在组中**B** ，微型驱动程序编写为使用 USBCAMD2 需要配置仅包含特定于设备的代码。 也就是说，如果使用 USBCAMD2，您可以集中精力实现支持的视频格式、 属性集、 映像解压缩和颜色空间转换。 USBCAMD2 微型驱动程序库用于控制连接到*stream.sys*类驱动程序和 USB 总线驱动程序，从而简化了开发照相机微型驱动程序的过程。

虽然与交互 USBCAMD2 *stream.sys*类的驱动程序，现已过时，开发与 USBCAMD2 照相机微型驱动程序可以是比通过编写您自己独立*stream.sys*类或 AVStream 微型驱动程序。

USBCAMD2 的主要目的是支持流式处理视频摄像机，如网络摄像机。 但是，USBCAMD2 还提供了支持使用 USB 大容量，中断传输管道，以捕获仍从照相机发送的图像。 此功能支持 USB 摄像机快照功能，仍可捕获帧。

如果您的照相机主要流式处理视频中，并选择性地提供快照功能，然后您只需编写 USBCAMD2 微型驱动程序。 混合相机 （照相机的主要拍照仍，但是，还可以流式传输视频） 的供应商编写 USBCAMD2 微型驱动程序以支持流式传输功能，并单独 Windows 图像采集 (WIA) 仍照相机的驱动程序以支持仍映像存储和管理。 有关 WIA 和支持捕获静止图像的数字照相机的详细信息，请参阅[Windows 图像采集驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)。

USBCAMD2 库支持使用等时 pipe(s)、 大容量 I/O pipe(s) 和/或中断管道的组合来传输数据流和控制设置的照相机。 USBCAMD2 支持实现以下 USB 管道配置的照相机：

-   在单个同步管道，同步信息，例如开始和结束视频或仍在数据流中嵌入的帧。 这些类型的照相机可以同时视频和仍帧通过同一个同步管道进行多路复用或重用为仍帧的各个视频帧。

-   与以前的配置，通过添加到注册的应用程序的外部触发器事件的信号通知中断管道相同。

-   与第一个配置，添加了两个相同大容量为控件的 I/O 管道，并从照相机检索仍帧。

-   两个等时管道。 一个管道流式处理数据和其他管道包含同步信息，如的开始和结束的视频或仍帧。 这些摄像机还可以同时视频和仍帧通过同一个同步管道进行多路复用或重用为仍帧的各个视频帧。

-   两个大容量 I/O 管道和一个可选中断管道。 一个大容量管道流视频和其他大容量管道仍将传输映像。 可选中断管道发出信号通知的注册的应用程序的外部触发器事件。

**请注意**   USBCAMD2 支持使用具有多个备用设置的单个 USB 接口的照相机。 备用的所有设置必须都具有相同类型和数量的管道。 在类型的数组中指定此信息[ **USBCAMD\_管道\_Config\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)传递给[ *CamConfigureEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)时初始化和配置照相机。

 

USB 1.1 设备可以连接到 USB 2.0 总线，而 USBCAMD2 仅支持 USB 1.1 相机的设备，并因此被限制为 USB 1.1 总线的最大吞吐量 (例如，同步数据传输在*完整*-高速模式)。 USBCAMD2 不支持 USB 2.0*高*-同步数据传输的速度模式。 但是，如果照相机实现批量传输管道，然后它无法受益于连接到 USB 2.0 总线没有更多可用的大容量传输带宽。

 

 




