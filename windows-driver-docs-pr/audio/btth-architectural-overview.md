---
title: Windows 蓝牙主控制器接口 (HCI) 体系结构概述
description: 本主题提供 Windows 8.1 支持的体系结构概述，以便在 (HCI) 上将音频数据重路由，绕过蓝牙主机控制器接口。
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 548bdb4ae4ed8fd2e7299e7f54fbe6ad68184c51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789341"
---
# <a name="windows-bluetooth-host-controller-interface-hci-architectural-overview"></a>Windows 蓝牙主控制器接口 (HCI) 体系结构概述


本主题提供 Windows 8.1 支持的体系结构概述，以便在 (HCI) 上将音频数据重路由，绕过蓝牙主机控制器接口。

从 Windows 8.1 开始，Microsoft 操作系统已更新为与低功率系统芯片 (SoC) 设计解决方案兼容。 新的 Windows 支持与基于 Intel 或基于 ARM 的 SoC 设计兼容。 这些新的低功耗设备将针对 "always on" 方案进行优化，因此，电池消耗较低是成功的关键因素。

SoC 体系结构使用通用异步接收方/发送器 (UART) 传输模式向/从蓝牙主机控制器传输数据。

由于 UARTs 不能提供时间敏感的数据传输，因此，) 绕过通道的同步 (连接必须除了 UART 之外实现，通过 I2S 或音频编解码器与蓝牙无线电之间的其他连接传输音频数据。 这意味着必须重新路由音频数据才能绕过蓝牙 HCI。 蓝牙 HCI，通常在电脑上用于传输音频数据。

需要注意的是，此功能只是卸载在 Windows 8.1 之前存在于 Windows 版本中的相同功能，因此从用户角度来看，蓝牙免提配置文件 (HFP) 在计算机或便携式计算机上的 Windows 上的

下图显示了一起使用来在 Windows 8.1 中提供此新支持的软件和硬件组件。

![显示软件和硬件组件的关系图，这些组件协同工作以为蓝牙绕过音频流提供 windows 支持。](images/btth-bypass-arch.png)

请注意，此 Windows 功能不支持使用高级音频分发配置文件 (A2DP) 绕过音频流式处理。 Windows 8 提供单独的 A2DP 配置文件驱动程序，该驱动程序通过标准蓝牙 HCI 完全支持音频功能，无需任何其他音频驱动程序。

 

 




