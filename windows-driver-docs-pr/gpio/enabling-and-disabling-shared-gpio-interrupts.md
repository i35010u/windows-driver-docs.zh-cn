---
title: 启用和禁用共享 GPIO 中断
description: 在某些情况下，中断请求两个或多个外围设备中的行可能会连接到同一个物理通用 I/O (GPIO) pin。 共享的中断行的 GPIO pin 通常配置为使用级别触发中断。
ms.assetid: F3C8F2B1-54BC-46A1-8AC2-50006E1156FF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da7b60329d7a78860c388ca909187210905abb8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326170"
---
# <a name="enabling-and-disabling-shared-gpio-interrupts"></a>启用和禁用共享 GPIO 中断


在某些情况下，中断请求两个或多个外围设备中的行可能会连接到同一个物理通用 I/O (GPIO) pin。 共享的中断行的 GPIO pin 通常配置为使用级别触发中断。

如果这些设备的驱动程序在此的 GPIO 插针，GPIO 框架扩展 (GpioClx) 将调用注册其中断服务例程 (Isr) 添加中断时触发[*客户端\_EnableInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh439377)回调函数仅当第一个驱动程序注册此中断。 GpioClx 时其他驱动程序注册以使用已启用的 GPIO 中断，在内部跟踪这些注册，但不会另外调用*客户端\_EnableInterrupt*启用此功能的回调函数中断。 同样，调用 GpioClx [*客户端\_DisableInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh439371)回调函数仅当最后一项注册驱动程序释放中断。

 

 




