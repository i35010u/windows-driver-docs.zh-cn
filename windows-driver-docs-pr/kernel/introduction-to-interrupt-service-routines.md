---
title: 中断服务例程简介
description: 中断服务例程简介
ms.assetid: e83eb873-7cdf-4faf-9a6e-cc5954ebf1d6
keywords:
- 中断服务例程 WDK 内核，关于 Isr
- Isr WDK 内核，关于中断服务例程
- InterruptService
- 基于行的中断 WDK 内核
- 中断线路 WDK 内核
- 消息-已发出信号中断 WDK 内核
- InterruptMessageService
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93e9545b199b9a5186b3bf49a63c10442fa935d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838624"
---
# <a name="introduction-to-interrupt-service-routines"></a>中断服务例程简介


接收中断的物理设备的驱动程序将注册一个或多个中断服务例程（ISR）来为中断服务。 系统每次收到该中断时都会调用 ISR。

PCI 2.2 之前的端口和总线设备生成*基于行的中断*。 设备通过将电气信号发送到称为*中断线路*的专用 pin 来生成中断。 Windows Vista 之前的 Microsoft Windows 版本仅支持基于行的中断。

从 PCI 2.2 开始，PCI 设备可以生成*消息信号中断*。 设备通过将数据值写入特定地址来生成消息信号中断。 Windows Vista 和更高版本的操作系统支持基于行和消息发出的中断。

系统支持两种不同类型的 Isr：

-   驱动程序可以注册[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程来处理基于行或消息发出的中断。 （这是 Windows Vista 之前唯一可用的类型。）系统传递驱动程序提供的上下文值。

-   驱动程序可以注册[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)例程来处理消息信号中断。 系统同时传递驱动程序提供的上下文值和中断消息的消息 ID。

有关注册 InterruptService 或 InterruptMessageService 例程以为设备中断提供服务的详细信息，请参阅[消息终止中断简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-message-signaled-interrupts)。
 

 




