---
title: USBCAMD2 照相机配置
description: USBCAMD2 照相机配置
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
ms.openlocfilehash: 58a8b181141f651c24217cacbe9bd2e8f35fd47e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841659"
---
# <a name="usbcamd2-camera-configurations"></a>USBCAMD2 照相机配置


支持 USB 摄像机的微型驱动程序可以是其前端和 USB 总线驱动程序上的*sys.databases*类驱动程序的客户端，如下图所示。

![说明 usb 摄像机微型驱动程序型号的示意图](images/usbimdev.png)

在**对关系图的组配置**进行分组时，微型驱动程序编写器必须与*stream*类驱动程序、照相机和 USB 总线交互。 在组**B**配置中，编写为使用 USBCAMD2 的微型驱动程序只需包含特定于设备的代码即可。 也就是说，如果使用 USBCAMD2，则可以集中精力实现对视频格式、属性集、图像解压缩和颜色空间转换的支持。 USBCAMD2 微型驱动程序库控制与*stream*类驱动程序和 USB 总线驱动程序的连接，从而简化了照相机微型驱动程序的开发过程。

尽管*USBCAMD2 类驱动程序的接口*现在已过时，但使用 USBCAMD2 开发照相机微型驱动程序比编写您自己的独立*Stream*类或 AVStream 微型驱动程序更容易。

USBCAMD2 的主要用途是支持流式处理视频摄像机，如网络摄像机。 但是，USBCAMD2 还支持使用 USB 大容量和中断传输管道捕获从照相机发送的静止图像。 此功能支持带有快照功能的 USB 照相机来捕获静止帧。

如果照相机主要流式传输视频，还可以提供快照功能，则只需编写 USBCAMD2 微型驱动程序。 混合相机的供应商（主要拍摄照片，但也可以流式传输视频的照相机）编写 USBCAMD2 微型驱动程序以支持流功能，并使用单独的 Windows 图像获取（WIA）驱动程序来支持静止图像存储和管理。 有关 WIA 和支持捕获静止图像的数字相机的详细信息，请参阅[Windows 映像获取驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)。

USBCAMD2 库支持使用同步管道、大容量 i/o 管道和/或中断管道组合的照相机来传输数据流和控制设置。 USBCAMD2 支持实现以下 USB 管道配置的照相机：

-   单个同步管道，其中包含同步信息，如视频的开头和结尾，以及嵌入在数据流中的静止帧。 这些类型的相机可以通过相同的同步管道对视频和静止帧进行多路复用，或重复使用单个视频帧作为静止帧。

-   与之前的配置相同，添加一个中断管道来向注册的应用程序发送外部触发器事件的通知。

-   与第一个配置相同，增加了两个批量 i/o 管道来控制和检索照相机中的静止帧。

-   两个同步管道。 一个管道流数据与另一个管道包含同步信息，如视频的开头和结尾或静止帧。 这些相机还可以通过相同的同步管道对视频和静止帧进行多路复用，或重复使用单个视频帧作为静止帧。

-   两个批量 i/o 管道和一个可选中断管道。 一个批量管道流视频和其他大容量管道传输仍为图像。 可选的中断管道向已注册的应用程序发出外部触发器事件的通知。

**请注意**   USBCAMD2 支持具有多个备用设置的单个 USB 接口的相机。 所有备用设置必须具有相同的管道类型和数量。 在初始化和配置照相机时传递到[*CamConfigureEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/nc-usbcamdi-pcam_configure_routine_ex)的类型为[**USBCAMD\_管道\_Config\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbcamdi/ns-usbcamdi-_pipe_config_descriptor)的数组中指定此信息。

 

尽管 USB 1.1 设备可以连接到 USB 2.0 总线，但 USBCAMD2 仅支持 USB 1.1 相机设备，因此限制为 USB 1.1 总线的最大吞吐量（例如，以*全速*模式传输同步数据）。 对于同步数据传输，USBCAMD2 不支持 USB 2.0*高速*模式。 但是，如果照相机仅实现批量管道，则它可以从连接到 USB 2.0 总线（其中有更多可用的大容量传输带宽）中受益。

 

 




