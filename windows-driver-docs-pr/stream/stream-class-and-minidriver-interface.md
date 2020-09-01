---
title: 流类和微型驱动程序接口
description: 流类和微型驱动程序接口
ms.assetid: d85510e6-1fd7-442a-bd88-f32b6c13ff75
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，流类接口
- 流式处理微型驱动程序 WDK Windows 2000 内核，流类接口
- 微型驱动程序 WDK Windows 2000 内核流式处理，流类接口
- 流类接口 WDK 流式处理微型驱动程序
- SRBs WDK 流式处理微型驱动程序
- Isr WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebe726ea40e51c08d75a41606507b00725f3b2af
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185537"
---
# <a name="stream-class-and-minidriver-interface"></a>流类和微型驱动程序接口





流类接口主要是类驱动程序和微型驱动程序之间的一组函数调用。 类驱动程序控制请求流，在需要访问适配器硬件时调用适配器微型驱动程序。 类驱动程序负责多处理器和中断同步。 在初始化类驱动程序和微型驱动程序后，微型驱动程序是被动的，只由类驱动程序调用。 大多数从微型驱动程序到类驱动程序的函数调用都是低级别的服务请求。

控制微型驱动程序的命令和信息的基本机制是 *流请求块* (SRB) 。 为每个微型驱动程序提供了一组 SRBs 来访问驱动程序的特定功能，通常特定于设备支持的每个数据流。 此信息通过大型循环缓冲区中的操作系统控制的 DMA 传递到设备。

SRB 包含一个命令和与该命令关联的数据。 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构包含与特定 SRB 相关的所有信息。 此结构（通常称为 SRB）包含用于补充命令的其他参数。

下图显示了在初始化期间 stream 类和微型驱动程序之间的交互。

![阐释在初始化期间流类和微型驱动程序之间的交互的关系图](images/stclassi.png)

所有流式处理的微型驱动程序函数都可以选择与微型驱动程序的中断服务例程同步， (ISR) ，这使得微型驱动程序 nonreentrant。 换言之，当在微型驱动程序中执行线程时，不会对微型驱动程序中的任何其他函数（包括 ISR）进行调用。 即使在多处理器 Windows NT/Windows 2000 系统上，此 nonreentrant 条件也适用，使微型驱动程序更易于编写。 Stream 类驱动程序通过以下方式实现此 nonreentrant 条件：屏蔽流式处理微型驱动程序 (的 IRQ，使用 KeSynchronizeExecution 在运行任何微型驱动程序的例程时使用**KeSynchronizeExecution**) 所有低优先级 irq。 有关同步的详细信息，请参阅 [微型驱动程序同步](minidriver-synchronization.md)。

流式处理微型驱动程序可以根据需要调用 WDM 系统服务。 但是，微型驱动程序不会分配设备对象，而是使用类驱动程序的设备对象进行系统调用。 大多数微型驱动程序不需要进行 WDM 系统调用，因为所有必要的功能都可从类驱动程序获得。

在 &gt; \_ 进行 WDM 系统服务调用（ [**StreamClassCallAtNewPriority**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscallatnewpriority) 例程除外）时，微型驱动程序必须知道所有微型驱动程序入口点均以 IRQL 调度级别调用。 此函数允许服务调用以 IRQL = 调度 \_ 级别或被动 \_ 级别，具体取决于指定的优先级。 通过在[**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构中将**TurnOffSynchronization**布尔值设置为**TRUE**，可以重写此对 IRQL 的限制。

 

