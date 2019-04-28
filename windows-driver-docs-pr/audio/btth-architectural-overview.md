---
title: Windows 蓝牙主控制器接口 (HCI) 体系结构概述
description: 本主题提供有关重新路由要绕过蓝牙主机的音频数据的 Windows 8.1 支持的体系结构概述控制器接口 (HCI)。
ms.assetid: FC9E5254-B543-4890-811C-1DA5F28E61B9
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60697fee2589d9b2d55f25b26f387e3b424cf404
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333908"
---
# <a name="windows-bluetooth-host-controller-interface-hci-architectural-overview"></a>Windows 蓝牙主控制器接口 (HCI) 体系结构概述


本主题提供有关重新路由要绕过蓝牙主机的音频数据的 Windows 8.1 支持的体系结构概述控制器接口 (HCI)。

从 Windows 8.1 开始，Microsoft 操作系统已更新为与低能耗片系统 (SoC) 设计解决方案兼容。 新的 Windows 支持适用于基于 Intel 的或基于 ARM 的 SoC 设计。 将"always on"方案中，针对优化这些新的低功耗设备，因此低电量消耗将成功的关键因素。

SoC 体系结构使用的通用异步接收器/转换器 (UART) 传输模式来传输数据传入和传出蓝牙主控制器。

由于 UARTs 不能提供敏感数据传输时间，面向同步连接 (SCO) 绕过通道必须实现除了 UART，音频编解码器和蓝牙无线之间 I2S 或某些其他连接通过传输音频数据。 这意味着，必须重新音频数据路由绕过蓝牙 HCI。 蓝牙 HCI 将通常用于在 Pc 上传输的音频数据。

务必要注意此功能只需卸载存在的 Windows 8.1 之前的 Windows 版本中，因此从用户角度来看有没有蓝牙免提上的配置文件 (HFP) SoC 之间不同的用例的相同功能和在 Windows 电脑或笔记本电脑上的蓝牙 HFP。

下图显示了协同工作，提供 Windows 8.1 中的此新支持的软件和硬件组件。

![关系图显示软件和硬件组件，它们共同协作以提供 windows 支持蓝牙绕过音频流。](images/btth-bypass-arch.png)

请注意，此 Windows 功能不支持绕过音频流使用的高级音频分发配置文件 (A2DP)。 Windows 8 提供完全支持通过标准蓝牙 HCI 的音频功能，无需任何其他的音频驱动程序的单独 A2DP 配置文件驱动程序。

 

 




