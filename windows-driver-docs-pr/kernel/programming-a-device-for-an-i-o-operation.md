---
title: 为 I/O 操作设备编程
description: 为 I/O 操作设备编程
keywords:
- 关键部分例程 WDK 内核
- I/o WDK 内核，设备编程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d81c7f5c3ef965d7dfdda63b3de34b9439d766a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805399"
---
# <a name="programming-a-device-for-an-io-operation"></a>为 I/O 操作设备编程





使用以下常规指导原则来设计、编写和调用为设备提供 i/o 操作的 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程：

-   为设备提供 i/o 操作计划的 *SynchCritSection* 例程必须尽快返回控制权。

    出于此原因， *SynchCritSection* 例程只应执行为 i/o 设置设备所需的操作。 因此，该驱动程序应执行所有 IRP 预处理，初始化其他驱动程序例程的状态信息，并在调用 *SynchCritSection* 例程之前获取硬件资源。

-   设备驱动程序可以有多个 *SynchCritSection* 例程来对设备进行编程。

    例如，设置读取请求的设备的驱动程序与设置某些设备控制请求明显不同，可能有单独的 *SynchCritSection* 例程来针对每种类型的请求对其设备进行编程。

-   每个 *SynchCritSection* 例程必须尽快返回控制权，因为运行任何 *SynchCritSection* 例程会阻止驱动程序的 ISR 执行。

    不应使用 **switch** 语句或使用多个嵌套 if if 来编写单个、大型、通用的 *SynchCritSection* 例程。 **then。else** 语句来确定要执行的操作或要更新的状态信息。 另一方面，应避免编写多个只计划一个设备注册的 *SynchCritSection* 例程。

 

