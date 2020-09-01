---
title: 使用 WmiFireEvent 发送事件
description: 使用 WmiFireEvent 发送事件
ms.assetid: f9cf8491-0f5a-4d83-849f-3edb77488092
keywords:
- WMI WDK 内核，事件跟踪
- 事件 WDK WMI
- 跟踪 WDK WMI
- 发送 WMI 事件
- 事件块 WDK WMI
- 通知 WDK WMI
- WmiFireEvent
- 动态实例名称 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e3a06ddeec0927aa3128c578fee254f81fe3617
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192905"
---
# <a name="sending-an-event-with-wmifireevent"></a>使用 WmiFireEvent 发送事件





驱动程序可以调用 [**WmiFireEvent**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent) 来发送不使用动态实例名称的事件，以及将静态实例名称基于单个基名称字符串或 PDO 的设备实例 ID。

事件必须是块的单个实例，即，驱动程序无法调用 **WmiFireEvent** 来发送由单个项或多个实例构成的事件。 若要发送此类事件，驱动程序必须调用 [**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)，如 [使用 IoWMIWriteEvent 发送事件](sending-an-event-with-iowmiwriteevent.md)中所述。

在 WMI 启用事件之前，驱动程序不应发送事件。 事件启用后，当事件的触发条件发生时，驱动程序将：

1.  从非分页池分配缓冲区，并将事件数据写入缓冲区。 如果事件没有数据，则驱动程序可以跳过此步骤。

2.  调用具有以下参数的 [**WmiFireEvent**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent) ：

    -   指向驱动程序的设备对象的指针

    -   指向表示事件块的 GUID 的指针

    -   如果事件块具有多个实例，则为该实例的索引

    -   如果要与事件一起发送数据，则为数据的字节数，或者，如果没有，则为0

    -   如果要随事件一起发送数据，则为指向包含数据的驱动程序分配的缓冲区的指针; 如果没有，则为 **NULL** 。

    驱动程序必须分配从非分页池传递到 **WmiFireEvent**的所有参数，包括事件数据缓冲区。 WMI 释放驱动程序分配的内存，而不会因驱动程序而进一步介入。

**WmiFireEvent**返回后，驱动程序将继续监视事件的触发条件，并在每次发生触发器条件时发送事件，直到 WMI 禁用该事件。

 

