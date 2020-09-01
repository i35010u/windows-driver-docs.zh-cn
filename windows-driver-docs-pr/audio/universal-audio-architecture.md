---
title: 通用音频体系结构
description: Microsoft 通用音频体系结构 (UAA) 使符合体系结构的音频设备完全依赖于操作系统以提供驱动程序支持。
ms.assetid: a42eff33-7952-4004-903d-9b202d1864b9
keywords:
- UAA WDK
- 通用音频体系结构 WDK
- 音频设备 WDK UAA
- PCI 音频适配器 WDK
- USB WDK 音频
- IEEE 1394 WDK 音频
- Intel 高质音频规范
- WDM 音频驱动程序 WDK，通用音频体系结构
- 音频驱动程序 WDK，通用音频体系结构
- 1394 WDK 音频
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9326b3ad161c7fc0c6e68c53cc3efa3959bb48f2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210317"
---
# <a name="universal-audio-architecture"></a>通用音频体系结构

Microsoft 通用音频体系结构 (UAA) 使符合体系结构的音频设备完全依赖于操作系统以提供驱动程序支持。

若要 UAA 兼容，PCI 音频适配器必须符合 Intel 高质音频规范，这是 Intel 音频编解码器 "97 (AC" 97) 规范的后续版本。 与 AC "97" 不同，intel 高质音频 ("Intel HD 音频") 可标准化总线控制器，以及 (将控制器连接到编解码器) 的链接的 "串行接口" 链接。 Intel HD 音频设备的 UAA 设计准则包含不属于 Intel 高质音频规范的其他要求。 Windows Vista 提供对 UAA 兼容 PCI 音频适配器的完整驱动程序支持。

若要 UAA 兼容，USB 音频设备必须符合 usb 音频规范和 USB 音频设备的 UAA 设计准则。 USB 音频设备可使用 [USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) ( # A0) ，它作为 Windows 的一部分提供。 按照定义，与 Windows 中的 USBAudio 类系统驱动程序兼容的 USB 音频设备符合 UAA。

要与 UAA 兼容，IEEE 1394 AV/C 音频设备必须符合 ieee 1394 AV/C 音频设备的相关 IEEE 1394 规范和 UAA 设计准则。 IEEE 1394 音频设备可使用 [AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver) ( # A0) ，它作为 Windows 的一部分提供。

有关 Microsoft UAA 计划的详细信息，请参阅 [通用音频体系结构](/previous-versions/windows/hardware/design/dn640534(v=vs.85)) 白皮书。

有关 Intel HD 音频的详细信息，请参阅 [INTEL Hd 音频](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) 网站。

有关 USB 和 IEEE 1394 音频设备的相关规范的列表，请参阅 [USBAudio 类系统驱动](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 程序和 [AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)。