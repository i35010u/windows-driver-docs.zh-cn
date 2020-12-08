---
title: 基于 USB 或 1394 的会议摄像机
description: 基于 USB 或 1394 的会议摄像机
keywords:
- 筛选器关系图配置 WDK 视频捕获、基于 USB 的视频会议照相机
- 筛选器关系图配置 WDK 视频捕获，基于1394的视频会议照相机
- 基于 USB 的视频会议照相机 WDK 视频捕获
- 基于1394的视频会议照相机 WDK 视频捕获
- 视频会议照相机 WDK 视频捕获
- 照相机 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cedd0ef7419d524227a69e9b476419f220019ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839185"
---
# <a name="usb-or-1394-based-conferencing-camera"></a>基于 USB 或 1394 的会议摄像机


简单的筛选器图包含一个捕获筛选器，该筛选器公开不带电视/广播功能的单个视频流。 基于 USB 和1394的视频会议照相机通常使用此配置。

下图演示了基于1394的视频会议照相机的可能的筛选器图形配置之一。

![说明基于1394的视频会议照相机的可能的筛选器图形配置之一的关系图](images/conferencing-camera-1394.gif)

**注意**  ：从相机的单个捕获流是通过智能 t 筛选器 (的用户模式 DirectShow 筛选器复制的) 提供单独的捕获和预览流。 执行此复制不需要微型驱动程序复制数据。

 

如果供应商符合 UVC 规范，则不需要为其基于 USB 的相机编写微型驱动程序。 Microsoft 为此类照相机提供 [USB 视频类驱动程序](usb-video-class-driver.md) 。 Microsoft 建议开发任何基于 USB 的新会议照相机硬件，以遵循 UVC 规范。

Microsoft 还提供了 [USBCAMD 微型驱动程序库](usbcamd-minidriver-library.md) 用于向后兼容。 但是，USBCAMD 接口已过时，并且 Microsoft 已不再进行进一步的开发。

 

 




