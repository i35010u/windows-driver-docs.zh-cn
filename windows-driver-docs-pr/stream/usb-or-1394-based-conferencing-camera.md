---
title: 基于 USB 或 1394 的会议摄像机
description: 基于 USB 或 1394 的会议摄像机
ms.assetid: 06097803-a124-4c9b-bdb4-cfd8648bc81d
keywords:
- 筛选图形配置 WDK 视频捕获，基于 USB 的视频会议摄像机
- 筛选图形配置 WDK 视频捕获，基于 1394年的视频会议摄像机
- 基于 USB 的视频会议摄像机 WDK 视频捕获
- 1394 基于视频会议摄像机 WDK 视频捕获
- 视频会议摄像机 WDK 视频捕获
- 照相机 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27a43b7473144cdd7440471dd12bd805f3f536a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382504"
---
# <a name="usb-or-1394-based-conferencing-camera"></a>基于 USB 或 1394 的会议摄像机


简单的筛选器关系图包含与没有电视/无线电收发器优化功能公开一个单一的视频流使用捕获筛选器。 基于 USB 的和基于 1394年的视频会议摄像机经常使用此配置。

下图演示了一个基于 1394年的视频会议摄像机的可能的筛选器图形配置。

![说明一种可能的筛选器图形配置的 1394年基于视频会议摄像机的关系图](images/conferencing-camera-1394.gif)

**请注意**  :单个捕获流从照相机复制由用户模式下 DirectShow 筛选器 （智能 Tee 筛选器） 提供单独的捕获和预览流。 而无需微型驱动程序可以将数据复制执行此复制。

 

供应商不需要编写用于其基于 USB 的相机微型驱动程序，如果它符合 UVC 规范。 Microsoft 提供了[USB 视频类驱动程序](usb-video-class-driver.md)用于此类相机。 Microsoft 建议开发任何新的基于 USB 的会议摄像机硬件，以遵循 UVC 规范。

Microsoft 还提供了[USBCAMD 微型驱动程序库](usbcamd-minidriver-library.md)为了向后兼容。 但是，USBCAMD 接口已过时，并且 Microsoft 已停止使用其进一步开发。

 

 




