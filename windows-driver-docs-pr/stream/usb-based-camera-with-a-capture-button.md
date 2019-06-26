---
title: 带捕获按钮的基于 USB 的摄像机
description: 带捕获按钮的基于 USB 的摄像机
ms.assetid: abbd824c-1ade-4dbc-8807-e558c444a3ea
keywords:
- 筛选器图形配置 WDK 视频捕获，基于 USB 的相机捕获按钮
- 仍然 pin WDK 视频捕获
- 捕获按钮 WDK AVStream
- 与基于 USB 的相机捕获按钮 WDK 视频捕获
- 仍捕获映像 WDK 视频捕获
- 仍捕获 WDK 视频捕获的映像
- 照相机 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b17b5a84e77abc3f92ce0bb3dcc1cdcd332a2dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377725"
---
# <a name="usb-based-camera-with-a-capture-button"></a>带捕获按钮的基于 USB 的摄像机


一个稍微复杂的筛选器关系图，相比[USB 或基于的 1394年会议摄像机](usb-or-1394-based-conferencing-camera.md)，为其微型驱动程序公开仍 pin 支持捕获静止图像的按钮的会议摄像机创建。 用户将一个按钮推送摄像机上时，仍处于 pin 可以提供更高分辨率图像。

供应商不需要编写用于其基于 USB 的相机微型驱动程序，如果它符合 UVC 规范。 Microsoft 提供了[USB 视频类驱动程序](usb-video-class-driver.md)用于此类相机。 Microsoft 建议开发任何新的基于 USB 会议摄像机硬件，以遵循 UVC 规范。

Microsoft 还提供了[USBCAMD 微型驱动程序库](usbcamd-minidriver-library.md)为了向后兼容。 USBCAMD 支持以仍插针相机。 但是，USBCAMD 接口已过时，并且 Microsoft 已停止使用进一步开发。

下图演示了基于 USB 的照相机，摄像机带有仍 pin 的可能的筛选器图形配置。

![说明使用仍 pin 基于 usb 的照相机的可能的筛选器图形配置的关系图](images/usb-camera-still.gif)

在图中，仍处于 pin 将流式传输单个映像时用户将推送到相机按钮。 或者，可以通过编程控制触发仍 pin。

生成上仍映像体系结构 (STI) 的 Windows 图像采集 (WIA) 技术是补充 USBCAMD 提供的功能。 请参阅[Windows 图像采集驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers)并[仍映像驱动程序](https://docs.microsoft.com/windows-hardware/drivers/image/still-image-drivers)有关详细信息。

WIA 视频快照筛选器是随 Microsoft Windows XP 和更高版本操作系统的 WIA 的补充。 WIA 视频快照筛选器仍使视频流中要捕获的帧。

有两种方法的捕获设备中的静止图像。 第一种是从捕获筛选器插入下游的 WIA 视频快照筛选器，并以编程方式触发捕获。 第二个是启用 pin 支持仍使用 USBCAMD 界面开发微型驱动程序。 然后可以通过在设备上按下按钮触发 WIA 视频快照筛选器。

而不是视频流仍处于 pin 从捕获映像的优点是可以提供更高分辨率图像并允许用户通过按按钮在设备上捕获映像仍 pin。

如果仍 pin 支持不会显式添加到微型驱动程序，WIA 视频快照筛选器可触发的软件，但解决方法将视频流相同。

一些仍的 pin 仅实现可以呈现后捕获 pin 中，因为它们基于捕获 pin 数据格式。

有关 WIA 驱动程序开发的详细信息，请参阅[仍映像技术](https://go.microsoft.com/fwlink/p/?linkid=8768)网站。

 

 




