---
title: 带捕获按钮的基于 USB 的摄像机
description: 带有 "捕获" 按钮的基于 USB 的相机
ms.assetid: abbd824c-1ade-4dbc-8807-e558c444a3ea
keywords:
- 筛选器关系图配置 WDK 视频捕获、带有捕获按钮的基于 USB 的摄像机
- 仍锁定 WDK 视频捕获
- 捕获按钮 WDK AVStream
- 带有 "捕获" 按钮的基于 USB 的相机视频捕获
- 捕获静止图像 WDK 视频捕获
- 仍在捕获 WDK 视频捕获的映像
- 照相机 WDK 视频捕获
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: cdf786c8c33a1203f0491853f9617b853af3a883
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191789"
---
# <a name="usb-based-camera-with-a-capture-button"></a>带有 "捕获" 按钮的基于 USB 的相机

与 [基于 USB 或1394的会议照相机](usb-or-1394-based-conferencing-camera.md)相比，创建的筛选器稍微稍微复杂一些，因为它的微型驱动程序公开的静止 pin 支持按钮来捕获静止图像。 当用户将相机上的按钮推送时，静止 pin 可以提供更高的分辨率图像。

如果供应商符合 UVC 规范，则不需要为其基于 USB 的相机编写微型驱动程序。 Microsoft 为此类照相机提供 [USB 视频类驱动程序](usb-video-class-driver.md) 。 Microsoft 建议开发任何新的基于 USB 的电话会议硬件，以遵循 UVC 规范。

Microsoft 还提供了 [USBCAMD 微型驱动程序库](usbcamd-minidriver-library.md) 用于向后兼容。 USBCAMD 支持具有静止 pin 的相机。 但是，USBCAMD 接口已过时，并且 Microsoft 已停止其开发。

下图演示了一个可能的筛选器图形配置，适用于带有静止 pin 的基于 USB 的相机。

![说明带静止 pin 的基于 usb 的相机可能的筛选器图形配置的示意图](images/usb-camera-still.gif)

在关系图中，当用户将该按钮推入照相机时，静止 pin 仅流式传输一个图像。 此外，也可以通过编程控制触发静态静态。

Windows 映像采集 (WIA) 技术构建于静态映像体系结构 (STI) 补充 USBCAMD 提供的功能。 有关详细信息，请参阅 [Windows 映像获取驱动程序](../image/windows-image-acquisition-drivers.md) 和 [静止映像驱动程序](../image/still-image-drivers.md) 。

WIA 视频快照筛选器是由 Microsoft Windows XP 和更高版本的操作系统随附的 WIA 的补充。 WIA 视频快照筛选器允许从视频流中捕获仍帧。

可通过两种方法从设备捕获静止图像。 第一种方式是插入从捕获筛选器下游的 WIA 视频快照筛选器并以编程方式触发捕获。 第二种方法是通过使用 USBCAMD 接口开发微型驱动程序来启用仍支持静止。 然后，可以通过在设备上推送按钮来触发 WIA 视频快照筛选器。

从静止 pin 捕获图像（而不是视频流）的优点是：静止 pin 可以提供更高的分辨率图像，并允许用户通过按设备上的按钮来捕获映像。

如果仍未将固定 pin 支持显式添加到微型驱动程序中，则该软件可能会触发 WIA 视频快照筛选器，但解析将与视频流相同。

某些静止 pin 实现只能在捕获 pin 后呈现，因为它们基于捕获 pin 数据格式。

有关 WIA 驱动程序开发的详细信息，请参阅 [映像设备驱动程序设计指南](../image/index.md)。