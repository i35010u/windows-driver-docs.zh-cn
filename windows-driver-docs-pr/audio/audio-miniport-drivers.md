---
title: 音频微型端口驱动程序
description: 音频微型端口驱动程序
ms.assetid: cf52759e-5da6-41a2-994d-4be15de9ae3d
keywords:
- WDM 音频驱动程序 WDK，微型端口驱动程序
- 音频驱动程序 WDK，微型端口驱动程序
- 音频的微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fc4006cd8350c30671975755beb639b32ac7e1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331463"
---
# <a name="audio-miniport-drivers"></a>音频微型端口驱动程序


## <span id="audio_miniport_drivers"></span><span id="AUDIO_MINIPORT_DRIVERS"></span>


本部分介绍音频微型端口驱动程序接口，并说明如何进行开发的音频硬件的寄存器是直接访问系统处理器的系统总线适配器驱动程序。 此类硬件包括所有 ISA/DMA、 PCMCIA 和 PCI 音频适配器。

本文档不讨论如何支持的外部总线上驻留的音频设备。 在外部总线上支持音频设备的信息，请参阅[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)并[AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)。

以下讨论假定读者熟悉流 (KS) 概念的内核。 有关背景信息，请参阅[内核流式处理](https://msdn.microsoft.com/library/windows/hardware/ff560842)。

WDM 音频驱动程序模型将 KS 筛选器的实现划分为互补而单独的端口和微型端口驱动程序。 这种划分使音频硬件驱动程序更轻松地编写通过隔离特定于设备的硬件接口问题的一般的筛选器实现问题。 硬件供应商编写微型端口驱动程序来直接控制其硬件设备，但使用操作系统提供了实现 KS 筛选器端口驱动程序。 通过定义完善的软件的接口彼此通信的端口和微型端口驱动程序。

以下主题中讨论了微型端口驱动程序开发的各个方面：

[端口类简介](introduction-to-port-class.md)

[支持设备](supporting-a-device.md)

[在内核中的 COM](com-in-the-kernel.md)

[适配器驱动程序构造](adapter-driver-construction.md)

[由操作系统的微型端口驱动程序类型](miniport-driver-types-by-operating-system.md)

[微型端口接口](miniport-interfaces.md)

[安装端口类音频适配器](installing-a-port-class-audio-adapter.md)

[端口驱动程序帮助程序对象](port-driver-helper-objects.md)

[音频设备的电源管理](power-management-for-audio-devices.md)

[音频驱动程序的版本号](version-numbers-for-audio-drivers.md)

[音频驱动程序的其他实现问题](other-implementation-issues-for-audio-drivers.md)

 

 




