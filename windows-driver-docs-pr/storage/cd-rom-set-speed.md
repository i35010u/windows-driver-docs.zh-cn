---
title: CD-ROM 设置速度
description: CD-ROM 设置速度
ms.assetid: 25a46b23-f823-4fc7-a370-cab1c9418a94
keywords:
- CD-ROM 驱动程序 WDK 存储
- 存储 cd-rom 驱动程序 WDK
- 电源管理 WDK cd-rom
- 加速 WDK CD-ROM
- 电池电量 WDK cd-rom
- 播放速度 WDK CD-ROM
- 纺锤速度 WDK 光盘
- 设置 CD 速度
- 设置流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88eccaddae806250717a2975a984c857185ca6d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841627"
---
# <a name="cd-rom-set-speed"></a>CD-ROM 设置速度


旋转光盘的速度通常比 cd-rom 驱动器所允许的最佳主轴速度要快。 例如，在便携式计算机中，高速旋转的 cd-rom 驱动器的速度很快就会耗尽电池。 可以将 cd-rom 驱动器设置为低速，以节省电池电量。

某些计算机不要求 CD-ROM 驱动器的运行速度较高。 例如，media center 计算机中的 CD-ROM 驱动器主要执行无需速度高于1X 的操作，如音频播放。 例如，在播放期间16X 的 CD-ROM 驱动器只需要1X 的速度时，可能会产生很大的干扰，导致用户体验不佳。

*Scsi-3 多媒体命令*（MMC）规范的第2版定义了用于设置 cd-rom 速度的两个命令：设置 cd 速度和设置流式处理。 在 Windows Vista 中，应用程序可以通过[**将 IOCTL 发送\_CDROM\_将\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed)请求发送到类驱动程序，指示 cd-rom 类驱动程序发出这两个命令之一。

若要将 SET CD 速度命令发送到 CD-ROM 设备，调用方将在 Cdrom 的**RequestType**成员中指定**CdromSetSpeed**的请求类型， [ **\_设置\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_set_speed)，\_cdrom\_设置\_速度。

若要将设置流命令发送到设备，调用方在[**cdrom\_设置\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_set_streaming)\_CDROM\_**集的输入**上指定**CdromSetStreaming**的请求类型\_快速.

如果应用程序使用 "设置 CD 速度" 命令更改了主轴速度，则当媒体更改时，设备将自动恢复为其默认速度。 如果应用程序使用 "设置流式处理" 命令更改了主轴速度，则介质的更改不会影响速度，除非调用方在 CDROM 的**持久**成员中指定了**FALSE**的值，\_将\_流式处理结构。

设置流式处理请求仅在符合 MMC 的设备上运行。 如果应用程序将此请求发送到与 MMC 不兼容的设备，则 cd-rom 类驱动程序将无法请求。

 

 




