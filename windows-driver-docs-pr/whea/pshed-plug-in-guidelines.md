---
title: PSHED 插件指南
description: PSHED 插件指南
keywords:
- 平台特定硬件错误驱动程序插件 WDK WHEA，指导原则
- PSHED 插件 WDK WHEA，指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bd3313e720b0f4855630f1a3e85c4960db799c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834815"
---
# <a name="pshed-plug-in-guidelines"></a>PSHED 插件指南


下面是 PSHED 插件必须遵循的准则列表。

-   对于更正后的错误，错误处理流程受限于对所有设备驱动程序施加的相同限制。  (Isr) 的中断服务例程不得执行25微秒以上的延迟过程调用 (Dpc) 不得执行超过100毫秒。 因此，PSHED 插件的回调函数以及 PSHED 插件的回调函数可能调用的任何固件例程，都不能在任意时段内执行。 对于未更正的错误，错误处理流可能会忽略这些限制，因为如果未指定优先级来处理错误条件，则系统处于可能出现数据丢失的状态。

-   PSHED 插件应该只与它已断言控制的硬件直接交互。 这意味着 PSHED 插件应该执行以下操作：
    -   声明与之交互的任何硬件资源的所有权，这些资源在结构上对操作系统可见。
    -   支持即插即用 (PnP) 如果可以重新定位与之交互的任何硬件资源。
    -   将所有交互与与相同硬件资源交互的所有其他软件或固件对操作系统不可见的任何硬件资源进行协调。
    -   仅与 PSHED 或低级别硬件错误处理程序不能操作的硬件资源交互 (LLHEH) 。 PSHED 插件只应操作特定于芯片组的寄存器，这些寄存器不属于由 LLHEH 操作的标准芯片组寄存器。

**注意**   平台固件不应对所有计算机资源进行绝对控制，这种情况通常适用于系统管理模式错误处理代码，因为在虚拟化或分区系统中，可能会将硬件分区为此假设为 false。

 

 

 




