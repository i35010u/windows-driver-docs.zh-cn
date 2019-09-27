---
title: 高清音频 DDI
description: 高清音频 DDI
ms.assetid: d471777c-0002-4caa-a06e-c58e449b7678
keywords:
- HD 音频
- 高清晰音频（HD 音频）
- WDM 音频驱动程序 WDK，HD 音频
- 音频驱动程序 WDK，HD 音频
- Intel 高质音频规范
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578a3b3c419359223b7be49dfec6a20a349c8716
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71319921"
---
# <a name="high-definition-audio-ddi"></a>高清音频 DDI


在 Windows Vista 中，Microsoft 将提供以下两个驱动程序作为操作系统的一部分：

-   用于管理 Intel 高质音频（HD 音频）总线接口控制器的总线驱动程序。

-   [通用音频体系结构](universal-audio-architecture.md)（UAA）类驱动程序，用于管理连接到 HD 音频控制器的 UAA 兼容音频编解码器（或可能有多个编解码器）。

Microsoft 还将为运行 Windows Server 2003 和 Windows XP 的系统开发类似的 HD 音频总线驱动程序和 UAA HD 音频类驱动程序。 有关 HD 音频控制器体系结构的信息，请参阅[INTEL HD 音频](https://go.microsoft.com/fwlink/p/?linkid=42508)网站上的 Intel 高质音频规范。 有关 Microsoft UAA 的概述，请参阅[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站上标题为通用音频体系结构的白皮书。

HD 音频总线驱动程序实现了 HD 音频设备驱动程序接口（DDI），其中内核模式音频和调制解调器驱动程序使用该接口与附加到 HD 音频控制器的硬件编解码器进行通信。 HD 音频总线驱动程序向其子级公开 HD 音频 DDI，这是管理编解码器的音频和调制解调器驱动程序的实例。

Windows Server 2003 和 Windows XP 上运行的 HD 音频总线驱动程序的版本支持 HD 音频 DDI 的三个变体：

-   [**HDAUDIO\_总线\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)结构定义的 DDI。 此 DDI 与 Windows Vista 中的 HD 音频 DDI 完全相同。

-   [**HDAUDIO\_总线\_接口V2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)结构定义的 DDI。 此 DDI 在 Windows Vista 和更高版本的 Windows 中可用。

-   [**HDAUDIO\_总线\_接口BDL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构定义的 DDI。 此 DDI 在 Windows XP 和更高版本的 Windows 中可用。

这三个 DDIs 之间的差别很小，并在[高清音频 DDI 版本之间的差异](differences-between-the-hd-audio-ddi-versions.md)中进行了介绍。

在 Windows Vista 中，HD 音频总线驱动程序支持 HDAUDIO\_总线\_接口和 HDAUDIO\_总线\_接口\_V2 结构定义的 DDI。

在 windows Vista、windows Server 2003 和 windows XP 中，UAA 类驱动程序使用 HDAUDIO\_总线\_接口结构定义的 DDI 来管理与 UAA 兼容的音频编解码器。 此外，硬件供应商可以选择编写使用其中一个或两个 DDIs 的自定义设备驱动程序来管理其音频和调制解调器编解码器。

硬件供应商应设计其音频编解码器，以符合 UAA 硬件要求文档（要发布）。 在缺少供应商提供的自定义音频驱动程序的情况下，用户可以依赖系统提供的 UAA HD 音频类驱动程序来管理与 UAA 兼容的音频编解码器。 但是，音频编解码器可能包含只能通过供应商的自定义驱动程序访问的专有功能。

本部分介绍了两个版本的 HD audio DDI 的以下信息：

-   Intel 高清音频体系结构和 Microsoft 的 UAA HD 音频类驱动程序的背景讨论。

-   使用这两种版本的 HD audio DDI 控制音频和调制解调器编解码器的编程指导原则。

本部分包括：

[HD 音频和 UAA](hd-audio-and-uaa.md)

[HD 音频 DDI 编程指南](programming-guidelines.md)

 

 




