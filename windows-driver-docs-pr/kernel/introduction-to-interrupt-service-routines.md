---
title: 中断服务例程简介
description: 中断服务例程简介
ms.assetid: e83eb873-7cdf-4faf-9a6e-cc5954ebf1d6
keywords:
- 中断服务例程 WDK 内核，有关 Isr
- Isr WDK 内核，有关中断服务例程
- InterruptService
- 基于行的中断 WDK 内核
- 中断行 WDK 内核
- 消息信号中断 WDK 内核
- InterruptMessageService
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d595cdac33579fa225695380362379b4a6e66e32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340975"
---
# <a name="introduction-to-interrupt-service-routines"></a>中断服务例程简介


接收中断的物理设备的驱动程序将注册一个或多个中断服务例程 (ISR) 服务中断。 系统调用 ISR 每次收到中断。

有关端口和低于 PCI 2.2 总线的设备生成*基于行的中断*。 设备通过称为对专用 pin 发送电气信号生成中断*中断行*。 在 Windows Vista 之前的 Microsoft Windows 版本仅支持基于行的中断。

从 PCI 2.2 开始，可以生成 PCI 设备*消息信号中断*。 设备的数据值写入到特定地址生成的消息信号中断。 Windows Vista 和更高版本操作系统支持基于行和消息信号中断。

系统支持两种不同类型的 Isr:

-   该驱动程序可以注册[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程来处理基于行或消息信号中断。 （这是唯一可用在 Windows Vista 之前的类型）。系统通过驱动程序提供的上下文值。

-   该驱动程序可以注册[ *InterruptMessageService* ](https://msdn.microsoft.com/library/windows/hardware/ff547940)例程来处理消息信号中断。 系统将驱动程序提供的上下文值和中断消息的消息 ID 传递。

 

 




