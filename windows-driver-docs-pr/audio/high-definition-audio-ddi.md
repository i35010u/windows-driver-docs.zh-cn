---
title: 高清音频 DDI
description: 高清音频 DDI
ms.assetid: d471777c-0002-4caa-a06e-c58e449b7678
keywords:
- 高清晰度音频
- 高清晰度音频 （HD 音频）
- WDM 音频驱动程序 WDK、 HD Audio
- 音频驱动程序 WDK、 HD Audio
- Intel 高清晰度音频规范
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94a6efb692b2b3697196b953f3e8c0faa4fe32c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333531"
---
# <a name="high-definition-audio-ddi"></a>高清音频 DDI


在 Windows Vista 中，Microsoft 将提供以下两个驱动程序作为操作系统的一部分：

-   用于管理 Intel 高清晰度音频 (HD Audio) 总线界面控制器的总线驱动程序。

-   一个[通用音频体系结构](universal-audio-architecture.md)(UAA) 类用于管理 UAA 符合音频编解码器 （或多个可能的编解码器） 的驱动程序连接到高清晰度音频控制器。

Microsoft 还将开发类似 HD Audio 总线驱动程序和运行 Windows Server 2003 和 Windows XP 的系统的 UAA HD Audio 类驱动程序。 HD Audio 控制器体系结构有关的信息，请参阅 Intel 高定义音频规范[Intel HD Audio](https://go.microsoft.com/fwlink/p/?linkid=42508)网站。 有关 Microsoft 的概述 UAA，请参阅白皮书标题为在通用音频体系结构[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站。

HD Audio 总线驱动程序实现高清晰度音频设备驱动程序接口 (DDI) 内核模式音频和调制解调器驱动程序用于与已附加到 HD Audio 控制器的硬件编解码器进行通信。 HD Audio 总线驱动程序公开 HD 音频 DDI 到其子元素，是管理编解码器的音频和调制解调器驱动程序的实例。

在 Windows Server 2003 和 Windows XP 上运行的 HD Audio 总线驱动程序版本支持 HD 音频 DDI 的三个变的体：

-   由定义 DDI [ **HDAUDIO\_总线\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff536413)结构。 此 DDI 等同于 HD 音频 DDI Windows Vista 中。

-   由定义 DDI [ **HDAUDIO\_总线\_接口\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)结构。 此 DDI 是在 Windows Vista 和更高版本的 Windows 中可用。

-   由定义 DDI [ **HDAUDIO\_总线\_接口\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416)结构。 此 DDI 现已推出 Windows XP 和更高版本的 Windows。

三个 DDIs 之间的差异很小的和中讨论[差异之间 HD 音频 DDI 版本](differences-between-the-hd-audio-ddi-versions.md)。

在 Windows Vista 中，HD Audio 总线驱动程序支持定义通过 HDAUDIO DDI\_总线\_界面和 HDAUDIO\_总线\_接口\_V2 结构。

在 Windows Vista、 Windows Server 2003 和 Windows XP 中，UAA 类驱动程序将使用 DDI 定义 HDAUDIO\_总线\_接口结构来管理符合 UAA 的音频编解码器。 此外，硬件供应商可以选择要编写使用一个或两个这些 DDIs 来管理其音频和调制解调器的编解码器的自定义设备驱动程序。

硬件供应商应该设计其音频编解码器以符合 UAA 硬件要求文档 （用于发布）。 如果没有从供应商的自定义音频驱动程序，用户可以依赖的系统提供 UAA HD 音频类驱动程序来管理其 UAA 符合音频编解码器。 但是，音频编解码器可能包含仅通过供应商的自定义驱动程序可以访问的专有功能。

本部分介绍这两个版本的 HD 音频 DDI 的以下信息：

-   Intel 的 HD Audio 体系结构和 Microsoft 的 UAA HD Audio 类驱动程序的背景讨论。

-   使用这两个版本的 HD 音频 DDI 来控制音频和调制解调器编解码器的编程指南。

本部分包括：

[HD 音频和 UAA](hd-audio-and-uaa.md)

[编程指南](programming-guidelines.md)

 

 




