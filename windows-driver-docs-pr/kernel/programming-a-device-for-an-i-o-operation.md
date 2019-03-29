---
title: 为 I/O 操作设备编程
description: 为 I/O 操作设备编程
ms.assetid: 952b07d8-81e3-40ec-8acd-be1143a7d2a2
keywords:
- 关键节例程 WDK 内核
- I/O WDK 内核设备编程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d00f776d44156e398b227077a9968b0a5e18550
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577170"
---
# <a name="programming-a-device-for-an-io-operation"></a>为 I/O 操作设备编程





遵循以下通用原则用于设计、 编写，并调用[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)程序设备的 I/O 操作的例程：

-   一个*SynchCritSection*程序适用于 I/O 操作的设备的例程必须尽可能快地返回控制。

    出于此原因， *SynchCritSection*例程应只能执行必要的操作来设置 I/O 设备。 因此，该驱动程序应执行所有的 IRP 预处理、 初始化、 其他驱动程序例程的状态信息以及调用之前获取的硬件资源*SynchCritSection*例程。

-   设备驱动程序可以有多个*SynchCritSection*例程进行编程的设备。

    例如，为其设置的读取请求明显不同设置某些设备控制请求设备的驱动程序可能具有单独*SynchCritSection*例程进行编程的每种类型的请求其设备。

-   每个*SynchCritSection*例程必须尽可能快速地返回控制，因为运行任何*SynchCritSection*例程阻止驱动程序的 ISR 执行。

    不应编写单一的大型、 常规用途*SynchCritSection*例程替换**切换**语句或多个嵌套**如果...然后...其他**语句，以确定它将执行哪些操作或要更新的状态信息。 但是，应避免编写大量*SynchCritSection*例程的程序只有单个设备注册。

 

 




