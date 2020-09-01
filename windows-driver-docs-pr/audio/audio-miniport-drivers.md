---
title: 音频微型端口驱动程序
description: 音频微型端口驱动程序
ms.assetid: cf52759e-5da6-41a2-994d-4be15de9ae3d
keywords:
- WDM 音频驱动程序 WDK，微型端口驱动程序
- 音频驱动程序 WDK，微型端口驱动程序
- 音频微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 320e0031e3909b0306b074d51f1fb56d739ea048
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208299"
---
# <a name="audio-miniport-drivers"></a>音频微型端口驱动程序


## <span id="audio_miniport_drivers"></span><span id="AUDIO_MINIPORT_DRIVERS"></span>


本部分介绍音频微型端口驱动程序接口，并说明如何开发音频硬件的适配器驱动程序，其寄存器可通过系统总线直接访问。 此类硬件包括所有 ISA/DMA、PCMCIA 和 PCI 音频适配器。

本文档不讨论如何支持驻留在外部总线上的音频设备。 有关在外部总线上支持音频设备的信息，请参阅 [USBAudio 类系统驱动](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 程序和 [AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)。

以下讨论假定读者熟悉内核流式处理 (KS) 概念。 有关背景信息，请参阅 [内核流式处理](../stream/kernel-streaming.md)。

WDM 音频驱动程序模型将 KS 筛选器的实现划分为互补但分离的端口和微型端口驱动程序。 这种划分使得音频硬件驱动程序更易于编写，方法是将泛型筛选器实现问题与设备特定的硬件接口问题隔离开来。 硬件供应商编写的微型端口驱动程序直接控制其硬件设备，但是，操作系统提供了实现 KS 筛选器的端口驱动程序。 端口和微型端口驱动程序通过定义完善的软件接口相互通信。

以下主题讨论了微型端口驱动程序开发的各个方面：

[端口类简介](introduction-to-port-class.md)

[支持某个设备](supporting-a-device.md)

[内核中的 COM](com-in-the-kernel.md)

[适配器驱动程序构造](adapter-driver-construction.md)

[按操作系统划分的微型端口驱动程序类型](miniport-driver-types-by-operating-system.md)

[微型端口接口](miniport-interfaces.md)

[安装端口类音频适配器](installing-a-port-class-audio-adapter.md)

[端口驱动程序帮助程序对象](port-driver-helper-objects.md)

[音频设备的电源管理](power-management-for-audio-devices.md)

[音频驱动程序的版本号](version-numbers-for-audio-drivers.md)

[音频驱动程序的其他实现问题](other-implementation-issues-for-audio-drivers.md)

 

