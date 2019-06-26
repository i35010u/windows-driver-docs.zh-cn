---
title: 启动视频微型端口驱动程序的设备
description: 启动视频微型端口驱动程序的设备
ms.assetid: e51a9483-eb12-4f7c-943f-075e670e97b1
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，启动设备
- 启动设备的微型端口驱动程序
- 设备初创企业 WDK 微型端口
- 微型端口驱动程序 WDK Windows 2000 中，初始化
- 初始化微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5af495bcee5aa2715a7f1a56904700c954f5ff7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376051"
---
# <a name="starting-the-device-of-the-video-miniport-driver"></a>启动视频微型端口驱动程序的设备


## <span id="ddk_starting_the_device_of_the_video_miniport_driver_gg"></span><span id="DDK_STARTING_THE_DEVICE_OF_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


PnP 管理器将发送 IRP 代码 (请参阅[IRP 主要函数代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)) 到视频端口驱动程序请求启动图形适配器。 视频端口驱动程序的调度例程调用微型端口驱动程序[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)响应此 IRP 代码例程。 某些详细信息*HwVidFindAdapter*的以下主题中讨论了任务：

[设置视频适配器的访问范围](setting-up-video-adapter-access-ranges.md)

[在注册表中设置的硬件信息](setting-hardware-information-in-the-registry.md)

[更改在适配器上的状态](changing-state-on-the-adapter.md)

 

 





