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
ms.openlocfilehash: 99e9720effb5636681dae6881c775d6e55c6178d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382655"
---
# <a name="providing-isr-context-information"></a>提供 ISR 上下文信息





ISR 进入时，接收到调用时，该驱动程序设置任何上下文区域的指针[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)注册该例程。

大多数驱动程序设置到该设备对象表示的物理设备的生成中断，或该设备对象的设备扩展的上下文指针。 驱动程序可以将驱动程序的 ISR 的状态信息存储在设备扩展中，并[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程，后者的通常执行几乎所有的 I/O 处理，以满足每个请求，导致要中断的设备。

通常情况下，驱动程序使用设备扩展将指针存储到每个设备的中断对象 (从调用返回**IoConnectInterruptEx**)。 驱动程序通常还允许以确定是否中断由 ISR 支持的设备颁发 ISR 的设备扩展中存储信息。

（或者，中断指针可以存储在驱动程序分配的非分页缓冲池的对象。）

 

 




