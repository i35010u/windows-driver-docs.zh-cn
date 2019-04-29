---
title: 释放设备和控制器对象
description: 释放设备和控制器对象
ms.assetid: 35404401-d3a8-4257-b1a3-b16ebe42b181
keywords:
- 卸载例程 WDK 内核，非 PnP 驱动程序
- 非即插即用卸载例程 WDK 内核
- 发布设备
- 释放控制器对象
- 设备版本 WDK 内核
- 控制器对象 WDK 内核，发布
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c12a6540d93822d262f4b687ffdd8de0214fa4e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324473"
---
# <a name="releasing-device-and-controller-objects"></a>释放设备和控制器对象





驱动程序中删除的设备或控制器对象之前，它必须释放对外部资源，如指针其他驱动程序的对象和/或中断的对象，它存储在相应的设备或控制器扩展到其引用。 然后，它可以调用[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)为每个驱动程序创建的设备对象。 一个非 WDM 驱动程序，以前称为[ **IoCreateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548395)还必须调用[ **IoDeleteController**](https://msdn.microsoft.com/library/windows/hardware/ff549078)。

自动为任何内核定义的对象，该驱动程序为其提供设备扩展中的存储时释放[*卸载*](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程调用**IoDeleteDevice**与相应的设备对象。 一般情况下，所有对象[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)或[*重新初始化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)例程通过调用设置**KeInitialize *Xxx*** 可以通过调用释放**IoDeleteDevice**如果驱动程序为该对象在其设备扩展中提供存储。 例如，如果驱动程序包含[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)例程和已提供存储在其设备扩展中，调用的必要 DPC 和计时器对象**IoDeleteDevice**释放这些系统资源。

同样，任何内核定义的对象，该驱动程序为其提供存储在控制器扩展将自动释放时*Unload*例程调用**IoDeleteController**与相应的控制器对象。

如果**DriverEntry**或*重新初始化*调用的例程[ **IoGetConfigurationInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549157)要递增的计数特定类型的设备*Unload*例程还必须调用**IoGetConfigurationInformation**和递减中适用于其设备的 I/O 管理器的全局配置的计数因为它的信息结构中删除相应的设备对象。

它将控制权，返回前*Unload*例程还负责释放的任何其他驱动程序分配资源尚未释放由其他驱动程序例程。

 

 




