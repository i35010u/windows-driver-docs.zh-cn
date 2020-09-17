---
title: 将 IOCTL 传送到视频微型端口驱动程序
description: 将 IOCTL 传送到视频微型端口驱动程序
ms.assetid: 9f9ad20e-d8cf-485d-adad-c04eeb40b705
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，IOCTLs
- IOCTLs WDK Windows 2000 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd53b414d013950eb7f001885956796a353ecd88
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716318"
---
# <a name="communicating-ioctls-to-the-video-miniport-driver"></a>将 IOCTL 传送到视频微型端口驱动程序


## <span id="ddk_communicating_ioctls_to_the_video_miniport_driver_gg"></span><span id="DDK_COMMUNICATING_IOCTLS_TO_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


下图显示了显示驱动程序如何使用 IOCTLs 与视频微型端口驱动程序通信。

![说明显示器驱动程序/视频微型端口驱动程序通信的示意图](images/dpy2.png)

显示驱动程序使用 IOCTL 调用 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) ，将同步请求发送到视频微型端口驱动程序。 对于输入和输出，GDI 使用单个缓冲区来将请求传递到 i/o 子系统。 I/o 子系统将请求路由到视频端口，此端口用于处理包含视频微型端口驱动程序的请求。

某些 IOCTL 请求要求微型端口驱动程序访问视频寄存器，其他 IOCTL 请求则存储或检索微型端口驱动程序的数据结构中的信息。 通常情况下，无请求需要视频微型端口驱动程序来执行实际的绘图操作。

一般情况下，除非是模块化的，否则显示驱动程序将处理绘图和其他时间关键操作。 将 IOCTL 发送到微型端口驱动程序以执行时间关键功能可能会降低系统性能。

有关系统定义的视频 IOCTLs 的说明，请参阅 [视频微型端口驱动程序 I/o 控制代码](/windows-hardware/drivers/ddi/index) 。 可以通过添加 *专用 IOCTL*（必须按 [定义 i/o 控制代码](../kernel/defining-i-o-control-codes.md)中所述的格式）来扩展显示驱动程序与视频微型端口驱动程序之间的接口。 如果需要编写新的 IOCTL，你应该首先与 Microsoft 技术支持联系。

 

