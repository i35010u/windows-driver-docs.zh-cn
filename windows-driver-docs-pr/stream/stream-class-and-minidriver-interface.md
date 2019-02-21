---
title: Stream 类和微型驱动程序接口
description: Stream 类和微型驱动程序接口
ms.assetid: d85510e6-1fd7-442a-bd88-f32b6c13ff75
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，流类接口
- 流式处理微型驱动程序 WDK Windows 2000 内核，流类接口
- 微型驱动程序 WDK Windows 2000 内核流式处理，流类接口
- 流类接口 WDK 流式处理微型驱动程序
- Srb WDK 流式处理微型驱动程序
- Isr WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a5cf4d56758ad2a33e650ddcdec10822b9b017e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542899"
---
# <a name="stream-class-and-minidriver-interface"></a>Stream 类和微型驱动程序接口





流类接口是主要的函数调用的类驱动程序和微型驱动程序之间的一组。 在类驱动程序控制请求流，需要访问适配器硬件时调用适配器的微型驱动程序。 在类驱动程序负责包含多个处理器和中断同步。 初始化类驱动程序和微型驱动程序后，微型驱动程序是被动单元，只能由类驱动程序调用。 函数调用微型驱动程序的类驱动程序的大部分都是低级别服务请求。

控制命令和信息写入微型驱动程序的基本机制是*流请求块*(SRB)。 Srb 一组为每个微型驱动程序可以访问特定功能的驱动程序提供，并通常特定于设备支持的每个数据流。 此信息将通过向设备操作系统系统控制在较大的循环缓冲区 DMA。

SRB 包含命令以及使用该命令关联的数据。 一个[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构包含与特定 SRB 相关的所有信息。 此结构，通常简称为 SRB，包含要补充该命令的其他参数。

下图显示了在初始化过程中的流类和微型驱动程序之间的交互。

![说明在初始化过程中的流类和微型驱动程序之间的交互的关系图](images/stclassi.png)

与微型驱动程序的中断服务例程 (ISR) 使 nonreentrant 微型驱动程序可以选择同步所有流式处理的微型驱动程序函数。 换而言之，微型驱动程序中执行某线程，当任何调用都将不进行中的任何其他函数微型驱动程序，包括 ISR 此 nonreentrant 条件为 true，即使在多处理器的 Windows NT/Windows 2000 系统，轻松地编写微型驱动程序上。 Stream 类驱动程序通过关闭流的微型驱动程序 （和所有较低优先级的 Irq） 使用的 IRQ 屏蔽，从而实现此 nonreentrant 条件**KeSynchronizeExecution**时在任何微型驱动程序的例程中执行代码。 有关同步的详细信息，请参阅[微型驱动程序同步](minidriver-synchronization.md)。

流式处理的微型驱动程序可以调用根据 WDM 系统服务。 但是，微型驱动程序不会分配一个设备对象，但使用的类驱动程序的设备对象发出系统调用。 大多数微型驱动程序不需要进行 WDM 系统调用，因为所有必要的功能是可从类驱动程序。

微型驱动程序必须注意所有微型驱动程序入口点调用在 IRQL&gt;调度\_级别 WDM 系统服务调用时，除[ **StreamClassCallAtNewPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff568230)例程。 此函数允许服务调用在 IRQL = 调度\_级别或被动\_级别，具体取决于指定的优先级。 IRQL 的这种限制可以通过设置重写**TurnOffSynchronization**中布尔[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)结构 **，则返回 TRUE**。

 

 




