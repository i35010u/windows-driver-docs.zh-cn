---
title: 处理事件
description: 处理事件
ms.assetid: 2cd7ccf3-12f5-4ad0-a7c9-a0f437b72445
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，事件
- 流式处理微型驱动程序 WDK Windows 2000 内核，事件
- 微型驱动程序 WDK Windows 2000 内核流式处理，事件
- 事件 WDK 流式处理微型驱动程序
- 事件设置 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 406a314e355560c2e3f80d1d235626e3f074133c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384023"
---
# <a name="handling-events"></a>处理事件





微型驱动程序可能支持事件集。 这两个整数和单个流的形式设备可能会收到请求，以启用或禁用事件。 类驱动程序句柄事件启用和禁用请求。 它使用单独的队列的每个流，并为设备队列每个已启用的事件。 如果禁用的事件，在类驱动程序会将其从队列删除。 请注意类驱动程序队列已启用的每个事件，是否微型驱动程序 does 其自己的同步。

微型驱动程序提供支持中的事件集**DeviceEventsArray**的成员[ **HW\_流\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)结构。 每个流提供支持中的事件集**StreamEventsArray**的[ **HW\_流\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)结构流。

微型驱动程序定义的事件集，它通过处理[ **KSEVENT\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_set)数据结构，又指向的数组[ **KSEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_item)结构，一个用于每个事件在事件集中。

微型驱动程序提供了[ *StrMiniEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_event_routine)可以接收事件请求，以及在设备自身的回调如果它可以接收事件请求每个流的回调例程。 如果*StrMiniEvent*例程将返回状态代码以外成功、 类驱动程序将排队事件。

当客户端发出的事件启用请求时，会传递[ **KSEVENTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)结构，其中介绍了如何事件应后会发生该事件信号，还可以后跟特定于事件的参数。 在类驱动程序收到请求时，它将构造[ **KSEVENT\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)结构来描述应触发该事件的方式。 队列 KSEVENT\_项结构的每个事件。 微型驱动程序可以使用[ **StreamClassGetNextEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassgetnextevent)例程，以检查事件队列。

当实际发生的事件时，微型驱动程序发出信号的类驱动程序通过调用[ **StreamClassDeviceNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassdevicenotification)或[ **StreamClassStreamNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification). 微型驱动程序可以发出事件信号以多种不同方式： 它可以发出信号发生特定事件，或者它可以发出信号发生特定类型的所有事件。 请参阅**StreamClassDeviceNotification**或**StreamClassStreamNotification**有关详细信息。

在类驱动程序可以分析[ **KSEVENTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)结构，以创建其[ **KSEVENT\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)结构，但它不能执行后面的原始请求中的所有特定于事件的参数相同。 微型驱动程序可以将额外的空间分配后 KSEVENT\_特定类型的事件，通过提供一个非零值的条目结构**ExtraEntryData** KSEVENT 成员\_项平时声明此事件。 当*StrMiniEvent*称为对于该类型的事件，它应在内存中存储来自 KSEVENTDATA 任何特定于事件的参数。

 

 




