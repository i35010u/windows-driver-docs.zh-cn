---
title: 事件对象
description: 事件对象
ms.assetid: da9df4a2-26cf-4861-80ca-1790ca059e45
keywords:
- 内核调度程序对象 WDK，事件对象
- 调度程序对象 WDK 内核，事件对象
- 事件对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52e8322c55a78d97d421f7d35717858b8136c20e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361980"
---
# <a name="event-objects"></a>事件对象





驱动程序可以使用一个事件对象等待下一步低驱动程序处理 IRP 等待驱动程序设置。 具有驱动程序创建的线程的驱动程序或驱动程序等待同步 I/O 请求完成的调度例程也可用于事件对象同步之间其线程和/或其他驱动程序例程的操作。

本部分包含以下主题：

[定义和使用一个事件对象](defining-and-using-an-event-object.md)

[标准事件对象](standard-event-objects.md)

 

 




