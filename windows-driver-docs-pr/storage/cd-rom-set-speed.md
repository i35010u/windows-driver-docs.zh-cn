---
title: CD-ROM 设置速度
description: CD-ROM 设置速度
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
ms.openlocfilehash: 7883fbe1ebd626cc9691b36143a209e60b90cbb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811783"
---
# <a name="cd-rom-set-speed"></a>CD-ROM 设置速度


旋转光盘的速度通常比 cd-rom 驱动器所允许的最佳主轴速度要快。 例如，在便携式计算机中，高速旋转的 cd-rom 驱动器的速度很快就会耗尽电池。 可以将 cd-rom 驱动器设置为低速，以节省电池电量。

某些计算机不要求 CD-ROM 驱动器的运行速度较高。 例如，media center 计算机中的 CD-ROM 驱动器主要执行无需速度高于1X 的操作，如音频播放。 例如，在播放期间16X 的 CD-ROM 驱动器只需要1X 的速度时，可能会产生很大的干扰，导致用户体验不佳。

 (MMC) 规范的第2版 *Scsi-3 多媒体命令* 定义了两个用于设置 cd-rom 速度的命令：设置 cd 速度和设置流式处理。 在 Windows Vista 中，应用程序可以通过向类驱动程序发送 [**IOCTL \_ CDROM \_ \_ 速度**](/windows-hardware/drivers/ddi/ntddcdrm/ni-ntddcdrm-ioctl_cdrom_set_speed) 请求，指示 cd-rom 类驱动程序发出这两个命令之一。

若要将 SET CD 速度命令发送到 CD-ROM 设备，调用方在对 IOCTL **CdromSetSpeed** cdrom **RequestType** 集速度的输入上指定了 [**CDROM \_ 集 \_ 速度**](/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_set_speed)的 RequestType 成员中的 CdromSetSpeed 请求类型 \_ \_ \_ 。

若要将设置流命令发送到设备，调用方在对 IOCTL **CdromSetStreaming** cdrom **RequestType** 集速度的输入上指定了 [**CDROM \_ 集 \_ 流式处理**](/windows-hardware/drivers/ddi/ntddcdrm/ns-ntddcdrm-_cdrom_set_streaming)的 RequestType 成员中的 CdromSetStreaming 请求类型 \_ \_ \_ 。

如果应用程序使用 "设置 CD 速度" 命令更改了主轴速度，则当媒体更改时，设备将自动恢复为其默认速度。 如果应用程序使用设置流命令更改了主轴速度，则介质的更改不会影响速度，除非调用方在 CDROM **FALSE** 集 **Persistent** \_ \_ 流式处理结构的永久成员中指定值 FALSE。

设置流式处理请求仅在符合 MMC 的设备上运行。 如果应用程序将此请求发送到与 MMC 不兼容的设备，则 cd-rom 类驱动程序将无法请求。

 

