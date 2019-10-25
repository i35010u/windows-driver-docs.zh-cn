---
title: 视频微型端口驱动程序的设备扩展（XDDM）
description: 视频微型端口驱动程序的设备扩展（Windows 2000 模型）
ms.assetid: 4d7841d1-39e2-4bdf-b79b-3feb363a0fe5
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，设备扩展
- 设备扩展 WDK 视频微型端口
- 扩展 WDK 视频微型端口
- 适配器状态 WDK 视频微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: dfa5bb113cc24451d2e115825fe3cbf8a0100e44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829192"
---
# <a name="video-miniport-drivers-device-extension-windows-2000-model"></a>视频微型端口驱动程序的设备扩展（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_s_device_extension_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_S_DEVICE_EXTENSION_WINDOWS_2000_MODEL__GG"></span>


设备扩展是每个微型端口驱动程序的主要区域，而只有全局存储区域用于特定于适配器的状态信息。

每个微型端口驱动程序定义其设备扩展的大小、内部结构和内容。 视频端口驱动程序将指向设备扩展的指针作为输入参数传递给每个系统定义的微型端口驱动程序函数（ **DriverEntry**和，如果已实现，则为[*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)和*SvgaHwIoPortXxx）* 函数。 许多**VideoPort**_Xxx_函数也需要此指针作为参数。

微型端口驱动程序还必须使用设备扩展来维护单个适配器的状态信息。 系统检测到的每个适配器都将在单独的设备扩展中维护单独的状态信息。 微型端口驱动程序不得使用全局变量来存储任何每个适配器的状态。 这对于提供无缝多监视器支持尤为重要。

 

 





