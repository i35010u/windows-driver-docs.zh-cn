---
title: USB 音频类系统驱动程序 (Usbaudio.sys)
description: USB 音频类系统驱动程序 (Usbaudio.sys) 是提供音频设备驱动程序支持与通用串行总线 (USB) 设备类定义音频设备符合 AVStream 微型驱动程序。
ms.assetid: 7ECE8006-3181-451C-B047-A3D767A7B98A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25eff07f09a55371fbdd3236e8f19ac7180d688b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354160"
---
# <a name="usb-audio-class-system-driver-usbaudiosys"></a>USB 音频类系统驱动程序 (Usbaudio.sys)


USB 音频类系统驱动程序 (Usbaudio.sys) 是提供音频设备驱动程序支持与通用串行总线 (USB) 设备类定义音频设备符合 AVStream 微型驱动程序。

## <span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>


音频设备规范 （版本 1.0） USB 设备类定义位于[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站。 Usbaudio.sys 支持 USB 音频规范中所述的功能的子集。 除了 Usbaudio.sys，还有几个其他内核模式音频组件在 Windows 驱动程序模型 (WDM)。 有关详细信息，请参阅[内核模式 WDM 音频组件](kernel-mode-wdm-audio-components.md)。

在 Windows 98 Usbaudio.sys 引入了对 USB 设备，例如扬声器和麦克风的支持。 在 Windows me.添加了对 MIDI 设备支持

当音频设备将自身标识为 USB 音频符合即插即用设备枚举期间时，系统会自动加载 USBAudio 驱动程序来驱动设备。 USBAudio 驱动器在设备直接，而无需专用适配器驱动程序的帮助。 这意味着符合 USB 音频规范的设备需要任何专有适配器驱动程序。

Microsoft 建议硬件供应商的 USB 音频设备而不是编写专有适配器驱动程序使用 USBAudio 驱动程序。

在 Windows 98 USBAudio 驱动程序支持以下功能：

-   所有类型 I 格式 （除了 8 位有符号 PCM)

-   Ac-3 II 格式

-   同步和自适应的同步类型

-   多渠道的设备

但是，在 Windows 98 USBAudio 不支持：

-   8 位有符号的 PCM 格式

-   MPEG II 格式

-   类型 III 格式

-   USB MIDI

-   [**WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)波形格式 (USBAudio 使用已打包的批\_格式\_24 位数据的 PCM 相反。)

在 Windows 98 第二个版本 (SE)、 Windows Me 和 Windows 2000 及更高版本，USBAudio 支持所有相同功能作为 Windows 98，有一个例外：USBAudio 支持 WAVEFORMATEXTENSIBLE，但不支持已打包的 WAVE\_格式\_24 位数据的 PCM。

在 Windows Me 和 Windows XP 和更高版本，USBAudio 支持在 Windows 98 SE 和 Windows 2000 中支持的所有功能。 此外，Windows Me 和 Windows XP 支持 USB MIDI，但不是支持 USB MIDI 元素。

下图显示了 USB 音频设备的驱动程序层次结构。 所有驱动程序组件图中显示由 Microsoft 中随操作系统一起提供。

![说明 usb 音频设备的驱动程序层次结构的关系图](images/usbaudio.png)

在图中的驱动程序组件有关的详细信息，请参阅以下各节：

[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)

[系统提供的 USB 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

 

 




