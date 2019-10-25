---
title: USB 音频类系统驱动程序 (Usbaudio.sys)
description: USB 音频类系统驱动程序（Usbaudio）是一种 AVStream 微型驱动程序，它为符合音频设备的通用串行总线（USB）设备类定义的音频设备提供驱动程序支持。
ms.assetid: 7ECE8006-3181-451C-B047-A3D767A7B98A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b5a0e8cc4e5088f88fde230e17d4ebf95423559
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830014"
---
# <a name="usb-audio-class-system-driver-usbaudiosys"></a>USB 音频类系统驱动程序 (Usbaudio.sys)


USB 音频类系统驱动程序（Usbaudio）是一种 AVStream 微型驱动程序，它为符合音频设备的通用串行总线（USB）设备类定义的音频设备提供驱动程序支持。

## <span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>


Usb 设备类定义音频设备规范（版本1.0）可在[Usb 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站上找到。 Usbaudio 支持 USB 音频规范中所述的功能的子集。 除了 Usbaudio 以外，Windows 驱动模型（WDM）中还有其他几个内核模式音频组件。 有关详细信息，请参阅[内核模式 WDM 音频组件](kernel-mode-wdm-audio-components.md)。

在 Windows 98 Usbaudio 中引入了对 USB 设备（如扬声器和麦克风）的支持。 Windows Me 中添加了对 MIDI 设备的支持。

当音频设备在即插即用设备枚举过程中将自身标识为符合 USB 音频的设备时，系统会自动加载 USBAudio 驱动程序来驱动设备。 USBAudio 直接驱动设备，无需借助专用适配器驱动程序。 这意味着，符合 USB 音频规范的设备不需要专用适配器驱动程序。

Microsoft 建议硬件供应商对其 USB 音频设备使用 USBAudio 驱动程序，而不是编写专用的适配器驱动程序。

在 Windows 98 中，USBAudio 驱动程序支持以下功能：

-   I 格式的所有类型（8位有符号 PCM 除外）

-   AC 3 类型 II 格式

-   同步和自适应同步类型

-   多通道设备

但是，Windows 98 中的 USBAudio 不支持：

-   8位有符号 PCM 格式

-   MPEG 类型 II 格式

-   类型 III 格式

-   USB MIDI

-   [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)波形格式（USBAudio 将\_格式的压缩波形用于24位数据的\_PCM。）

在 Windows 98 第二版（SE）、Windows Me 和 Windows 2000 及更高版本中，USBAudio 支持与 Windows 98 相同的功能，但有一种例外： USBAudio 支持 WAVEFORMATEXTENSIBLE，但不支持为24位\_PCM\_格式的压缩波形数据.

在 Windows Me 和 Windows XP 及更高版本中，USBAudio 支持 Windows 98 SE 和 Windows 2000 支持的所有功能。 此外，Windows Me 和 Windows XP 支持 USB MIDI，但不支持 USB MIDI 元素。

下图显示了 USB 音频设备的驱动程序层次结构。 图中所示的所有驱动程序组件都由 Microsoft 提供操作系统。

![说明 usb 音频设备驱动程序层次结构的示意图](images/usbaudio.png)

有关图中的驱动程序组件的详细信息，请参阅以下部分：

[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)

[系统提供的 USB 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




