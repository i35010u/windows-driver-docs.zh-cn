---
title: 事件对象
description: 事件对象
keywords:
- 内核调度程序对象 WDK，事件对象
- 调度程序对象 WDK 内核，事件对象
- 事件对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb0238739d418d5fb791706d139b7bd1d7f2426b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836939"
---
# <a name="event-objects"></a>事件对象





驱动程序可以使用事件对象等待，而下一个较低的驱动程序通过等待驱动程序处理 IRP 设置。 如果驱动程序的驱动程序创建的线程或驱动程序调度例程等待同步 i/o 请求完成，则还可以使用事件对象来同步其线程和/或其他驱动程序例程之间的操作。

本节包含下列主题：

[定义和使用事件对象](defining-and-using-an-event-object.md)

[标准事件对象](standard-event-objects.md)

 

 




