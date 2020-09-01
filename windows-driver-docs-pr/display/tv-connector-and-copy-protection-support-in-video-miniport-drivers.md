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
ms.openlocfilehash: 53aae2f7925ce38719cfef37a14944cf3b07aff2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067168"
---
# <a name="tv-connector-and-copy-protection-support-in-video-miniport-drivers"></a>视频微型端口驱动程序中的电视连接器和复制保护支持

具有电视连接器的适配器的视频微型端口驱动程序必须使用[**IOCTL \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) i/o 控制代码处理[**VRPs**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) 。 此 IOCTL 将发送到微型端口驱动程序，以查询 TV 连接器的功能和当前设置，并复制保护硬件或设置电视连接器和复制保护硬件的功能。 微型端口驱动程序通过检查[**VIDEOPARAMETERS**](/windows/desktop/api/tvout/ns-tvout-_videoparameters)结构的**dwCommand**字段来确定要执行的操作，该字段传递在 VRP 的**InputBuffer**中。 如果微型端口驱动程序未处理此 VRP，则系统将不允许) 受保护的 Dvd 上播放 (Rovi。

如果将**dwCommand**设置为 VP \_ 命令 \_ GET，并且设备*不*支持电视输出，则微型端口驱动程序 \_ 在 VRP 的**STATUSBLOCK**的**Status**成员中不应返回任何错误。 它还应将 VRP 的**StatusBlock**的**信息**成员设置为 VIDEOPARAMETERS 结构的大小（以字节为单位）。 它应将 **dwFlags** 设置为零，将 **dwTVStandard** 设置为 "副总裁" \_ 电视 \_ 标准 \_ win \_ VGA，并将 **dwAvailableTVStandard** 设置为 "副总裁 \_ 电视 \_ standard \_ win vga" \_ 。

如果**dwCommand**设置为 VP \_ 命令 \_ GET，并且设备支持 TV *does*输出，则微型端口驱动程序应通过在**dwFlags**成员中设置相应的标志并为与集标志相对应的其他结构成员指定值，在 VIDEOPARAMETERS 结构中指出这一点。

以下部分提供了具有 TV 连接器的设备的微型端口驱动程序的实现细节：

[查询电视连接器和复制保护硬件](querying-tv-connector-and-copy-protection-hardware.md)

[设置复制保护硬件](setting-copy-protection-hardware.md)

 

