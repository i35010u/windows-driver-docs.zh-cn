---
title: 提供 ISR 上下文信息
description: 提供 ISR 上下文信息
ms.assetid: 216c3111-3638-4410-a720-ff3d65a1eadd
keywords:
- 中断服务例程 WDK 内核，上下文信息
- Isr WDK 内核，上下文信息
- 中断对象 WDK 内核，上下文信息
- 上下文信息 WDK 中断
- 指针 WDK 中断
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83fa074f3ecb83b4b590d947e73de14d3d4e66c5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189516"
---
# <a name="providing-isr-context-information"></a>提供 ISR 上下文信息





进入时，ISR 接收指向驱动程序在调用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 时设置的任何上下文区域的指针，以注册例程。

大多数驱动程序将上下文指针设置为表示生成中断的物理设备的设备对象，或设置为该设备对象的设备扩展。 在设备扩展中，驱动程序可以存储驱动程序的 ISR 和 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程的状态信息，后者通常执行几乎所有的 i/o 处理以满足导致设备中断的每个请求。

通常，驱动程序使用设备扩展来存储指向每个设备中断对象的指针， (从对 **IoConnectInterruptEx**) 的调用返回。 驱动程序通常还会将信息存储在设备扩展中，以允许 ISR 确定由 ISR 支持的设备是否发出了中断。

 (或者，中断对象指针可以存储在驱动程序分配的非分页池中。 ) 

 

