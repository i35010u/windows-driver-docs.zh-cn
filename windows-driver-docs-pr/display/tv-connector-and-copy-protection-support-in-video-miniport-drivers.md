---
title: 视频微型端口驱动程序中的电视连接器和复制保护
description: 视频微型端口驱动程序中的电视连接器和复制保护支持
ms.assetid: 7d7d44b5-3248-4bee-bc4d-e02fd3c606a7
keywords:
- 视频微型端口驱动程序 WDK Windows 2000、电视连接器
- 视频微型端口驱动程序 WDK Windows 2000，复制保护支持
- 电视连接器 WDK 视频微型端口
- 复制保护 WDK 视频微型端口
- IOCTL_VIDEO_HANDLE_VIDEOPARAMETERS
- 复制保护 WDK 视频微型端口，关于复制保护支持
- 硬件 WDK 复制保护
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 419d42bd08e3625da76dbea68fdd3d88f47dd984
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825421"
---
# <a name="tv-connector-and-copy-protection-support-in-video-miniport-drivers"></a>视频微型端口驱动程序中的电视连接器和复制保护支持

具有电视连接器的适配器的视频微型端口驱动程序[**必须使用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) [**IOCTL\_视频\_处理\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) i/o 控制代码。 此 IOCTL 将发送到微型端口驱动程序，以查询 TV 连接器的功能和当前设置，并复制保护硬件或设置电视连接器和复制保护硬件的功能。 微型端口驱动程序通过检查[**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)结构的**dwCommand**字段来确定要执行的操作，该字段传递在 VRP 的**InputBuffer**中。 如果微型端口驱动程序未处理此 VRP，则系统将不允许播放 Rovi （以前称为 Macrovision）受保护的 Dvd。

如果**dwCommand**设置为副总裁\_命令\_GET，并且设备*不*支持电视输出，则微型端口驱动程序应在 VRP 的**STATUSBLOCK**的**Status**成员中不返回\_错误。 它还应将 VRP 的**StatusBlock**的**信息**成员设置为 VIDEOPARAMETERS 结构的大小（以字节为单位）。 它应将 " **dwFlags** " 设置为零，将 " **dwTVStandard** " 设置为 "副总裁"\_TV\_STANDARD\_WIN\_VGA，并将**dwAvailableTVStandard**设置为 "副总裁\_\_\_STANDARD\_

如果**dwCommand**设置为 VP\_命令\_GET，*并且设备支持*TV 输出，则微型端口驱动程序应通过在**dwFlags**成员中设置相应的标志并通过为与集标志相对应的其他结构成员赋值。

以下部分提供了具有 TV 连接器的设备的微型端口驱动程序的实现细节：

[查询电视连接器和复制保护硬件](querying-tv-connector-and-copy-protection-hardware.md)

[设置复制保护硬件](setting-copy-protection-hardware.md)

 

 





