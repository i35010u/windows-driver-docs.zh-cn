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
ms.openlocfilehash: f94cc6d46cd0c0fdb9c2fc4c8fed9603ef522810
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385856"
---
# <a name="registering-and-enabling-an-iotimer-routine"></a>注册和启用 IoTimer 例程





任何驱动程序可以注册[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)例程中，通过调用创建一个或多个设备对象后[**最好**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializetimer)。 该驱动程序可以通过调用启动计时器[ **IoStartTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostarttimer)。 下图说明了这些调用。

![关系图说明如何使用 iotimer 例程](images/3iotmer.png)

在调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)若要创建设备对象，驱动程序可以调用**最好**的入口点及其*IoTimer*例程，以及指向驱动程序创建的设备对象和驱动程序在其中维护任何上下文的上下文区域及其*IoTimer*例程使用。 I/O 管理器将设备对象与内核分配计时器对象相关联，并每隔一秒设置超时计时器对象。

驱动程序调用后**IoStartTimer**，将其*IoTimer*直到驱动程序调用的第二个每一次调用例程[ **IoStopTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostoptimer)。 驱动程序可以重新启用对调用其*IoTimer*例程替换**IoStartTimer**。 (通常情况下，当驱动程序调用**IoStartTimer**，它会提供从当前 IRP 的 I/O 堆栈位置获取的设备对象指针。)

在进入时， *IoTimer*例程传递设备对象指针<em>，</em>以及上下文指针，该驱动程序提供时调用它**最好**。

驱动程序不能调用**IoStopTimer**内*IoTimer*例程。

I/O 管理器中注销指定的设备对象的计时器例程和驱动程序调用时将释放及其关联的上下文[ **IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)。

 

 




