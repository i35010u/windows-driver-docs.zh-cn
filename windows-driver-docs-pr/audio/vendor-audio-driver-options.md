---
title: 供应商音频驱动程序选项
description: 供应商音频驱动程序选项
ms.assetid: 4306c027-28ae-4299-83c0-29d892bf64ca
keywords:
- WDM 音频驱动程序 WDK，供应商选项
- 音频驱动程序 WDK，供应商选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b5c7c3789db267533e211852f9f4b44ebb68516
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534171"
---
# <a name="vendor-audio-driver-options"></a>供应商音频驱动程序选项


## <span id="vendor_audio_driver_options"></span><span id="VENDOR_AUDIO_DRIVER_OPTIONS"></span>


若要利用的音频设备的内置系统支持，Microsoft 建议供应商使用以下项之一：

-   端口类适配器驱动程序 (请参阅[音频微型端口驱动程序](audio-miniport-drivers.md)) 的 ISA 或 PCI 适配器卡

-   USB 音频类驱动程序 (请参阅[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)) 为 USB 音频设备

-   自定义的 IEEE 1394 设备驱动程序 (请参阅[AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)) 的 IEEE 1394 音频设备

但是，如果这些选项并不足够，供应商可以实现以下项之一：

-   专有 KS 筛选器 (请参阅[KS 筛选器](https://msdn.microsoft.com/library/windows/hardware/ff567644))

-   Microsoft 不建议专有 KS 筛选器，因为它们是很难实现，且不必要的大多数 ISA、 PCI 和 USB 设备。

-   Stream 类微型驱动程序 (请参阅[流式处理微型驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff568277))

-   Microsoft 不建议专有流类微型驱动程序，因为它难以实现，但也可以是适用于集成音频和视频的设备。

提供的驱动程序支持的音频设备的可用选项的深入介绍，请参阅[WDM 音频驱动程序入门](getting-started-with-wdm-audio-drivers.md)。

 

 




