---
title: 流类和微型驱动程序接口
description: 流类和微型驱动程序接口
ms.assetid: d85510e6-1fd7-442a-bd88-f32b6c13ff75
keywords:
- Stream .sys 类驱动程序 WDK Windows 2000 内核，stream 类接口
- 流式处理微型驱动程序 WDK Windows 2000 内核，流类接口
- 微型驱动程序 WDK Windows 2000 内核流式处理，流类接口
- 流类接口 WDK 流式处理微型驱动程序
- SRBs WDK 流式处理微型驱动程序
- Isr WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44aaf8add9a36e99462f792ca90312425a439447
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837692"
---
# <a name="stream-class-and-minidriver-interface"></a>流类和微型驱动程序接口





流类接口主要是类驱动程序和微型驱动程序之间的一组函数调用。 类驱动程序控制请求流，在需要访问适配器硬件时调用适配器微型驱动程序。 类驱动程序负责多处理器和中断同步。 在初始化类驱动程序和微型驱动程序后，微型驱动程序是被动的，只由类驱动程序调用。 大多数从微型驱动程序到类驱动程序的函数调用都是低级别的服务请求。

控制微型驱动程序的命令和信息的基本机制是*流请求块*（SRB）。 为每个微型驱动程序提供了一组 SRBs 来访问驱动程序的特定功能，通常特定于设备支持的每个数据流。 此信息通过大型循环缓冲区中的操作系统控制的 DMA 传递到设备。

SRB 包含一个命令和与该命令关联的数据。 [**HW\_流\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构包含与特定 SRB 相关的所有信息。 此结构（通常称为 SRB）包含用于补充命令的其他参数。

下图显示了在初始化期间 stream 类和微型驱动程序之间的交互。

![阐释在初始化期间流类和微型驱动程序之间的交互的关系图](images/stclassi.png)

所有流式处理微型驱动程序函数都可以选择与微型驱动程序的中断服务例程（ISR）同步，从而使微型驱动程序 nonreentrant。 换言之，当在微型驱动程序中执行线程时，不会对微型驱动程序中的任何其他函数（包括 ISR）进行调用。 即使在多处理器 Windows NT/Windows 2000 系统上，此 nonreentrant 条件也适用，使微型驱动程序更易于编写。 当代码在任何微型驱动程序的例程中执行时，stream 类驱动程序将使用**KeSynchronizeExecution**屏蔽流式处理微型驱动程序（和所有低优先级 irq）的 IRQ 来实现此 nonreentrant 条件。 有关同步的详细信息，请参阅[微型驱动程序同步](minidriver-synchronization.md)。

流式处理微型驱动程序可以根据需要调用 WDM 系统服务。 但是，微型驱动程序不会分配设备对象，而是使用类驱动程序的设备对象进行系统调用。 大多数微型驱动程序不需要进行 WDM 系统调用，因为所有必要的功能都可从类驱动程序获得。

微型驱动程序必须知道，在进行 WDM 系统服务调用（ [**StreamClassCallAtNewPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscallatnewpriority)例程除外）时，所有微型驱动程序入口点均以 IRQL &gt; 调度\_级别进行调用。 此函数允许以 IRQL = 调度的服务调用\_级别或被动\_级别，具体取决于指定的优先级。 可以通过将[**HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构中的**TurnOffSynchronization**布尔值设置为**TRUE**，来重写此 IRQL 的限制。

 

 




