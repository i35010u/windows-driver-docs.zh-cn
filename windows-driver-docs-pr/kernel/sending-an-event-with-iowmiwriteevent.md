---
title: 使用 IoWMIWriteEvent 发送事件
description: 使用 IoWMIWriteEvent 发送事件
ms.assetid: 77c1041a-340c-4c59-a30a-e946adf60a95
keywords:
- WMI WDK 内核，事件跟踪
- 事件 WDK WMI
- 跟踪 WDK WMI
- 发送 WMI 事件
- 事件块 WDK WMI
- 通知 WDK WMI
- IoWMIWriteEvent
- 动态实例名称 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc23686ac6a69769cdb4d379078632084501838
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190035"
---
# <a name="sending-an-event-with-iowmiwriteevent"></a>使用 IoWMIWriteEvent 发送事件





驱动程序可以调用 [**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent) 来发送任何事件。 事件可以包含单个项、单个实例或数据块的所有实例，并且它可以使用动态实例名称。

与通过查询或更改请求（由 WMI 分配并部分初始化）传递的 **WNODE \_ * xxx*** 结构不同，驱动程序必须分配和初始化包含事件的 **WNODE \_ * XXX*** 结构的所有成员。

只有在 WMI 发送了 [**IRP \_ MN \_ enable \_ EVENTS**](./irp-mn-enable-events.md) 请求以启用事件之后，驱动程序才必须发送事件。 然后，当发生事件的触发条件时，驱动程序将：

1. 从非分页池分配一个缓冲区，以包含事件所需的 **WNODE \_ * XXX*** 结构，其中包括变量数据的空间（如果有）。

   根据事件的不同，驱动程序可能会为该事件分配一个 [**WNODE \_ 单个 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)、一个 [**WNODE \_ 单一 \_ 实例**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)或一个 [**WNODE 的 \_ 所有 \_ 数据**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data) 。 **WNODE \_ * XXX*** 加变量数据的大小不得超过注册表定义的1k 限制。

2. 初始化 **WNODE \_ * XXX*** 结构的所有成员，包括 **WnodeHeader**：

   - 驱动程序设置 **WNODE \_ 标志 \_ 事件 \_ 项** 标志以指示该结构是事件。

   - 驱动程序将设置下列标志之一来指示 **WNODE \_ * XXX*** 结构的类型：

     **WNODE \_ 标志 \_ 所有 \_ 数据**

     **WNODE \_ 标志 \_ 单一 \_ 实例**

     **WNODE \_ 标志 \_ 单一 \_ 项**

   - 驱动程序设置或清除下列标志，以指示块是使用静态还是动态实例名称：

     **WNODE \_ 标记 \_ 静态 \_ 实例 \_ 名称**

     **WNODE \_ 标记 \_ PDO \_ 实例 \_ 名称**

   - 驱动程序可以根据事件设置其他标志。

3. 将指向 **WNODE \_ * XXX*** 的指针转换为 PWNODE \_ 事件 \_ 项。

4. 通过指针调用 **IoWMIWriteEvent** 。

   如果 **IoWMIWriteEvent** 成功完成，WMI 将释放该事件的驱动程序分配内存。

[**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)返回后，驱动程序将继续监视事件的触发器条件，并在每次发生其触发器条件时发送事件，直到 WMI 发送[**IRP \_ MN \_ disable \_ EVENTS**](./irp-mn-disable-events.md)请求来禁用该事件。

如果事件的大小超过注册表定义的最大值 1K)  (，则驱动程序应使用初始化的[**WNODE \_ 事件 \_ 引用**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)（该引用指定事件的 GUID、其大小及其实例索引 (为动态实例名称) 或名称 (）调用**IoWmiWriteEvent** 。 WMI 将使用 **WNODE \_ 事件 \_ 引用** 中的信息来查询事件。

驱动程序可以通过调用 WMI 库例程 [**WmiFireEvent**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)，发送不使用动态实例名称并由单个实例组成的事件。 驱动程序无需为**WmiFireEvent**调用分配和初始化**WNODE \_ * XXX*** 结构。 WMI 将驱动程序的事件数据打包到 [**WNODE \_ 单一 \_ 实例**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance) 中，并将其传递给数据使用者。 有关使用 **WmiFireEvent**发送事件的详细信息，请参阅 [使用 WmiFireEvent 发送事件](sending-an-event-with-wmifireevent.md)。

 

