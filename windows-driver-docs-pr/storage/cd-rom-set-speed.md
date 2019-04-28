---
title: CD-ROM 设置速度
description: CD-ROM 设置速度
ms.assetid: 25a46b23-f823-4fc7-a370-cab1c9418a94
keywords:
- CD-ROM 驱动程序 WDK 存储
- 存储 CD-ROM 驱动程序 WDK
- 电源管理 WDK CD-ROM
- 速度 WDK CD-ROM
- 电池电量 WDK CD-ROM
- 播放速度 WDK CD-ROM
- 主轴转速 WDK CD-ROM
- 设置 CD 的速度
- 设置流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c2fcd248faa5737cdeab70295bfb0df63570a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338327"
---
# <a name="cd-rom-set-speed"></a>CD-ROM 设置速度


通常很方便地旋转 CDs 小于最佳主轴转速 CD-ROM 驱动器允许的速度。 例如，便携式计算机在快速启动的 CD-ROM 驱动器消耗电池的速度非常快。 可以将 CD-ROM 驱动器设置为较低的速度，节省电池电量。

某些计算机不需要 CD-ROM 驱动器以高的速度运行。 例如，在 media center 计算机 CD-ROM 驱动器主要执行不需要速度高于 1 X 的操作，例如音频播放。 在该数值调节钮的 CD-ROM 驱动器，例如，在播放，16 X 时仅 1 倍的速度是必需的可以生成会导致不良用户体验的大噪音。

版本 2 *scsi-3 多媒体命令*(MMC) 规范定义了用于设置 CD-ROM 速度的两个命令：设置 CD 速度和设置流式处理。 在 Windows Vista 中，应用程序可以通过发送指示 CD-ROM 类驱动程序问题，这两个命令之一[ **IOCTL\_CDROM\_设置\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff559381)对类驱动程序的请求。

若要发送到 CD-ROM 设备设置 CD 速度命令，调用方指定的请求类型**CdromSetSpeed**中**RequestType**的成员[ **CDROM\_设置\_速度**](https://msdn.microsoft.com/library/windows/hardware/ff551368)，在输入到 IOCTL\_CDROM\_设置\_速度。

若要将设置流式处理命令发送到设备，调用方指定的请求类型**CdromSetStreaming**中**RequestType**的成员[ **CDROM\_设置\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/ff551369)，在输入到 IOCTL\_CDROM\_设置\_速度。

如果应用程序更改主轴转速使用设置 CD 速度命令，设备会自动返回到其默认速度更改媒体时。 如果应用程序更改主轴转速使用设置流式处理命令，媒体的更改不会影响速度，除非调用方指定的值，否则**FALSE**中**的永久**CDROM 的成员\_设置\_流式处理结构。

设置流式处理请求仅适用于 MMC 合规的设备。 如果应用程序将此请求发送到设备不合规 MMC，CD-ROM 类驱动程序将无法发送请求。

 

 




