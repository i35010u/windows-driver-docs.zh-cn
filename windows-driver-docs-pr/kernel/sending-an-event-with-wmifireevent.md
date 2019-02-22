---
title: 发送具有 WmiFireEvent 的事件
description: 发送具有 WmiFireEvent 的事件
ms.assetid: f9cf8491-0f5a-4d83-849f-3edb77488092
keywords:
- WMI WDK 内核事件跟踪
- WDK WMI 事件
- 跟踪 WDK WMI
- 发送的 WMI 事件
- 事件阻止 WDK WMI
- 通知 WDK WMI
- WmiFireEvent
- 动态实例名称 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd6ae6b9dda93810b374e1160a852fde64ffd8d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542309"
---
# <a name="sending-an-event-with-wmifireevent"></a>发送具有 WmiFireEvent 的事件





驱动程序可以调用[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)发送事件，不要使用动态实例名称和的基础单个基名称字符串或 PDO 的设备实例 ID 的静态实例名称。

事件必须是一个块的单个实例 — 也就是说，调用一个驱动程序不能**WmiFireEvent**发送事件的单个项或多个实例组成。 若要发送此类事件，驱动程序必须调用[ **IoWMIWriteEvent**](https://msdn.microsoft.com/library/windows/hardware/ff550520)，如中所述[发送与 IoWMIWriteEvent 事件](sending-an-event-with-iowmiwriteevent.md)。

驱动程序不应发送事件，直到 WMI 启用了该事件。 启用事件后，事件的触发器条件时，该驱动程序：

1.  分配从非分页缓冲池的缓冲区，并将事件数据写入到缓冲区。 如果事件没有任何数据，该驱动程序可以跳过此步骤。

2.  调用[ **WmiFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff565807)使用以下参数：

    -   指向驱动程序的设备对象的指针

    -   指向表示事件块的 GUID 的指针

    -   如果事件块都有多个实例，该实例的索引

    -   如果要使用发送事件、 数据的字节数或 0 如果无数据

    -   如果数据将发送与事件，指向包含的数据驱动程序分配的缓冲区的指针或**NULL**如果没有，则

    驱动程序必须分配所有参数传递给**WmiFireEvent**，包括非分页缓冲池中的事件数据缓冲区。 WMI 释放由驱动程序而无需进一步干预的驱动程序分配内存。

之后**WmiFireEvent**返回时，驱动程序将继续监视事件的触发器条件及其触发条件发生之前 WMI 禁用该事件每次发送该事件。

 

 




