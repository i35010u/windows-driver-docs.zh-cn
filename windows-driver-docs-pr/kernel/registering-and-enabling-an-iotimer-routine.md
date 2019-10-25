---
title: 注册和启用 IoTimer 例程
description: 注册和启用 IoTimer 例程
ms.assetid: d06a6430-5098-492a-8114-d6f390083718
keywords:
- IoTimer
- IoInitializeTimer
- IoStartTimer
- 注册 IoTimer 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8ebb185831571dafbb1622a248df4f054f0ccf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838470"
---
# <a name="registering-and-enabling-an-iotimer-routine"></a>注册和启用 IoTimer 例程





任何驱动程序在创建一个或多个设备对象后，都可以通过调用[**IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)来注册[*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程。 然后，该驱动程序可以通过调用[**IoStartTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostarttimer)启动计时器。 下图说明了这些调用。

![演示如何使用 iotimer 例程的关系图](images/3iotmer.png)

在调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)以创建设备对象之后，驱动程序可以使用其*IoTimer*例程的入口点调用**IoInitializeTimer** ，同时还可以使用指向驱动程序创建的设备对象和上下文区域（其中的驱动程序维护其*IoTimer*例程使用的上下文。 I/o 管理器将设备对象与内核分配的计时器对象相关联，并将 timer 对象设置为每秒超时。

驱动程序调用**IoStartTimer**后，每秒调用一次*IoTimer*例程，直到驱动程序调用[**IoStopTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostoptimer)。 驱动程序可以使用**IoStartTimer**重新启用对其*IoTimer*例程的调用。 （通常情况下，当驱动程序调用**IoStartTimer**时，它将提供从当前 IRP 的 i/o 堆栈位置获取的设备对象指针。）

进入时，会向*IoTimer*例程传递设备对象指针<em>，</em>以及驱动程序在调用**IoInitializeTimer**时提供的上下文指针。

驱动程序不得从*IoTimer*例程中调用**IoStopTimer** 。

当驱动程序调用[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)时，i/o 管理器将注销指定设备对象的计时器例程，并释放其关联的上下文。

 

 




