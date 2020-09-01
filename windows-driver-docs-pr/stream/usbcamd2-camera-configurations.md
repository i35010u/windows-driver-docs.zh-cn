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
ms.openlocfilehash: 7b1f69636c6be12a3a9035a4e5b249d8d229c1bd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187659"
---
# <a name="usbcamd2-camera-configurations"></a>USBCAMD2 相机配置


支持 USB 摄像机的微型驱动程序可以是其高端和 USB 总线驱动程序上 *stream.sys* 类驱动程序的客户端，如下图所示。

![说明 usb 摄像机微型驱动程序型号的示意图](images/usbimdev.png)

在 **对关系图的配置进行** 分组时，微型驱动程序编写器必须对 *stream.sys* 类驱动程序、照相机和 USB 总线进行接口。 在组 **B** 配置中，编写为使用 USBCAMD2 的微型驱动程序只需包含特定于设备的代码即可。 也就是说，如果使用 USBCAMD2，则可以集中精力实现对视频格式、属性集、图像解压缩和颜色空间转换的支持。 USBCAMD2 微型驱动程序库控制与 *stream.sys* 类驱动程序和 USB 总线驱动程序的连接，从而简化了照相机微型驱动程序的开发过程。

尽管使用 *stream.sys* 类驱动程序的 USBCAMD2 接口现在已过时，但使用 USBCAMD2 开发照相机微型驱动程序比编写自己的独立 *stream.sys* 类或 AVStream 微型驱动程序更容易。

USBCAMD2 的主要用途是支持流式处理视频摄像机，如网络摄像机。 但是，USBCAMD2 还支持使用 USB 大容量和中断传输管道捕获从照相机发送的静止图像。 此功能支持带有快照功能的 USB 照相机来捕获静止帧。

如果照相机主要流式传输视频，还可以提供快照功能，则只需编写 USBCAMD2 微型驱动程序。 混合相机的供应商 (照相机，这些照相机主要拍摄照片，但也可以流式传输视频) 编写 USBCAMD2 微型驱动程序以支持流式处理功能，并使用单独的 Windows 映像获取 (WIA) 仍支持静止图像存储和管理。 有关 WIA 和支持捕获静止图像的数字相机的详细信息，请参阅 [Windows 映像获取驱动程序](../image/windows-image-acquisition-drivers.md)。

USBCAMD2 库支持使用同步管道 (s) 、大容量 i/o 管道 () 和/或中断管道组合的照相机来传输数据流和控制设置。 USBCAMD2 支持实现以下 USB 管道配置的照相机：

-   单个同步管道，其中包含同步信息，如视频的开头和结尾，以及嵌入在数据流中的静止帧。 这些类型的相机可以通过相同的同步管道对视频和静止帧进行多路复用，或重复使用单个视频帧作为静止帧。

-   与之前的配置相同，添加一个中断管道来向注册的应用程序发送外部触发器事件的通知。

-   与第一个配置相同，增加了两个批量 i/o 管道来控制和检索照相机中的静止帧。

-   两个同步管道。 一个管道流数据与另一个管道包含同步信息，如视频的开头和结尾或静止帧。 这些相机还可以通过相同的同步管道对视频和静止帧进行多路复用，或重复使用单个视频帧作为静止帧。

-   两个批量 i/o 管道和一个可选中断管道。 一个批量管道流视频和其他大容量管道传输仍为图像。 可选的中断管道向已注册的应用程序发出外部触发器事件的通知。

**注意**   USBCAMD2 支持具有多个备用设置的单个 USB 接口的相机。 所有备用设置必须具有相同的管道类型和数量。 在初始化和配置照相机时传递到[*CamConfigureEx*](/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)的[**USBCAMD \_ 管道 \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)类型的数组中指定此信息。

 

尽管 USB 1.1 设备可以连接到 USB 2.0 总线，但 USBCAMD2 仅支持 USB 1.1 相机设备，因此限制为 USB 1.1 总线 (的最大吞吐量，例如，以 *全速*模式) 的同步数据传输。 对于同步数据传输，USBCAMD2 不支持 USB 2.0 *高速*模式。 但是，如果照相机仅实现批量管道，则它可以从连接到 USB 2.0 总线（其中有更多可用的大容量传输带宽）中受益。

 

