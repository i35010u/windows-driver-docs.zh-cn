---
title: 其他标准驱动程序例程
description: 其他标准驱动程序例程
keywords:
- 驱动对象 WDK 内核
- 标准驱动程序例程 WDK 内核，驱动程序对象
- 驱动程序例程 WDK 内核，驱动程序对象
- 例程的 WDK 内核，驱动程序对象
- 对象 WDK 驱动程序对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7027c0fb4b51b13ba81d1bd1d361be8b70b40277
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803543"
---
# <a name="other-standard-driver-routines"></a>其他标准驱动程序例程





如 [驱动程序对象简介](introduction-to-driver-objects.md) 中的图示所示，内核模式驱动程序具有其他标准例程以及它们在各自的驱动程序对象中设置入口点的。 大多数标准驱动程序例程及其使用的某些依赖于配置的对象由 i/o 管理器定义。 使用包含 "custom" 一词的名称（包含 "custom" 一词）的驱动器对象图中显示的 ISR、 *SynchCritSection* 例程和名称由 NT 内核定义。

大多数驱动程序使用其创建的每个设备对象的 [设备扩展](device-extensions.md) 来维护有关其 i/o 操作的特定于设备的状态，并存储指向其必须分配的任何系统资源的指针，以便具有其他标准例程。 例如，驱动程序对象图中显示的 **DDCustomTimerDpc** 例程需要驱动程序为内核定义的计时器和 DPC 对象提供存储。

对 [驱动程序对象的介绍](introduction-to-driver-objects.md) 中，在图中左侧显示的最低级别驱动程序的标准驱动程序例程集与较高级别的驱动程序的设置不同。 此图中所示的某些例程是依赖于设备或依赖于配置的要求。 其他选项是可选的：可以根据驱动程序的设备的性质或配置、驱动程序的设计以及驱动程序在分层驱动程序链中的位置，来执行此类例程。

 

 




