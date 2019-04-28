---
title: PSHED 插件指南
description: PSHED 插件指南
ms.assetid: 2d17ebef-9474-4825-be09-c924ebd60c44
keywords:
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，准则
- PSHED 插件 WDK WHEA 准则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4aacc852492a32b1d3ae8c815ac8cc4cdba73b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340737"
---
# <a name="pshed-plug-in-guidelines"></a>PSHED 插件指南


下面是必须后跟 PSHED 插件的指南的列表。

-   对于已更正错误，错误处理流受到相同所有设备驱动程序施加的限制。 中断服务例程 (Isr) 必须执行不超过 25 种的微秒数和延缓的过程调用 (Dpc) 必须执行不超过 100 个微秒为单位。 因此，PSHED 插件的回调函数，以及任何固件例程 PSHED 插件的回调函数可能调用，必须执行任意长时间。 对于未更正的错误，错误处理流可以忽略这些限制，因为系统处于如果优先级不提供给处理错误条件可能发生数据丢失的状态。

-   PSHED 插件仅应直接与硬件进行交互，它具有通过添加控件。 这意味着 PSHED 插件应以下操作：
    -   声明的与它交互的任何硬件资源的所有权会对操作系统体系结构上可见。
    -   可以重新定位支持插 (PnP) 如果有与它交互的硬件资源。
    -   协调与体系结构上看不到与所有其他软件或固件与相同的硬件资源交互的操作系统的任何硬件资源的所有交互。
    -   仅与已不操作通过 PSHED 或低级别的硬件错误处理程序 (LLHEH) 的硬件资源进行交互。 PSHED 插件应仅处理不是由 LLHEH 操作的标准芯片组寄存器的一部分的芯片集特定寄存器。

**请注意**  平台固件不应假定绝对控制所有计算机资源，如通常是用于系统管理模式下的错误处理代码，这种情况，因为硬件可能会在虚拟化或已分区系统中，分区的方式，这种假设是 false。

 

 

 




