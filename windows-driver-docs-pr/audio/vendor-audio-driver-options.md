---
title: 供应商音频驱动程序选项
description: 供应商音频驱动程序选项
keywords:
- WDM 音频驱动程序 WDK，供应商选项
- 音频驱动程序 WDK，供应商选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb2e841aaf768c7686c6593445efa1088eee0401
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800463"
---
# <a name="vendor-audio-driver-options"></a>供应商音频驱动程序选项


## <span id="vendor_audio_driver_options"></span><span id="VENDOR_AUDIO_DRIVER_OPTIONS"></span>


为了充分利用音频设备的内置系统支持，Microsoft 建议供应商使用以下各项之一：

-   端口类适配器驱动程序 (参阅适用于 ISA 或 PCI 适配器的 [音频微型端口驱动程序](audio-miniport-drivers.md)) 

-   USB 音频类驱动程序 (参阅 [USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)) 用于 USB 音频设备

-   自定义 IEEE 1394 设备驱动程序 (参阅 [AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)) 用于 IEEE 1394 音频设备

但是，如果这些选项不足，则供应商可以实现以下其中一项：

-   专用 KS 筛选器 (参见 [KS 筛选](../stream/ks-filters.md) 器) 

-   Microsoft 不建议使用专用 KS 筛选器，因为它们难以实现，并且对于大多数 ISA、PCI 和 USB 设备都是不必要的。

-   Stream 类微型驱动程序 (参阅 [流式处理微型驱动程序](../stream/streaming-minidrivers2.md)) 

-   Microsoft 不建议使用专有的流类微型驱动程序，因为它很难实现，尽管它可能适用于集成音频和视频的设备。

有关为音频设备提供驱动程序支持的可用选项的深入讨论，请参阅 [使用 WDM 音频驱动程序入门](getting-started-with-wdm-audio-drivers.md)。

 

