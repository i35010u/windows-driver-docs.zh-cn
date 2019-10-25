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
ms.openlocfilehash: 91a3be7e12a573646a8e038f57cc02fd1b1bf8c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836364"
---
# <a name="sending-an-event-with-iowmiwriteevent"></a>使用 IoWMIWriteEvent 发送事件





驱动程序可以调用[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)来发送任何事件。 事件可以包含单个项、单个实例或数据块的所有实例，并且它可以使用动态实例名称。

与**WNODE\_* xxx*** 结构传递的查询或更改请求（由 WMI 分配并部分初始化）不同，驱动程序必须分配并初始化**WNODE\_* XXX*** 结构的所有成员，其中包含引发.

只有在 WMI 发送了[**IRP\_MN\_启用\_EVENTS**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)请求以启用事件之后，驱动程序才必须发送事件。 然后，当发生事件的触发条件时，驱动程序将：

1. 从非分页池分配一个缓冲区，以包含事件所需的**WNODE\_* XXX*** 结构，其中包括变量数据的空间（如果有）。

   根据事件的不同，驱动程序可能会分配[**WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)、 [**WNODE\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)或[**WNODE\_事件的所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)。 **\_WNODE**的大小不能超过注册表定义的1k 限制（1k）。

2. 初始化**WNODE\_* XXX*** 结构的所有成员，包括**WnodeHeader**：

   - 驱动程序将**WNODE\_标志设置为\_事件\_ITEM**标志，以指示结构是事件。

   - 驱动程序将设置下列标志之一来指示 WNODE 的类型 **\_* XXX*** 结构：

     **\_所有\_数据的 WNODE\_标志**

     **\_单一\_实例的 WNODE\_标志**

     **WNODE\_标记\_单一\_项**

   - 驱动程序设置或清除下列标志，以指示块是使用静态还是动态实例名称：

     **WNODE\_标记\_静态\_实例\_名称**

     **WNODE\_标记\_PDO\_实例\_名称**

   - 驱动程序可以根据事件设置其他标志。

3. 将指向**WNODE\_* XXX*** 的指针转换为 PWNODE\_事件\_项。

4. 通过指针调用**IoWMIWriteEvent** 。

   如果**IoWMIWriteEvent**成功完成，WMI 将释放该事件的驱动程序分配内存。

[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)返回后，驱动程序将继续监视事件的触发器条件，并在每次发生其触发器条件时发送事件，直到 WMI 发送[**IRP\_MN\_禁用\_EVENTS**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)请求禁用该事件。

如果事件的大小超过注册表定义的最大值1K （不推荐），驱动程序应使用初始化的 WNODE\_事件调用**IoWmiWriteEvent** ，该[**事件\_引用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)指定事件的 GUID、大小和实例索引（对于静态实例名称）或名称（适用于动态实例名称）。 WMI 将使用**WNODE\_事件\_引用**中的信息来查询事件。

驱动程序可以通过调用 WMI 库例程[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)，发送不使用动态实例名称并由单个实例组成的事件。 驱动程序无需为**WmiFireEvent**调用分配和初始化**WNODE\_* XXX*** 结构。 WMI 将驱动程序的事件数据打包到[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)中，并将其传递给数据使用者。 有关使用**WmiFireEvent**发送事件的详细信息，请参阅[使用 WmiFireEvent 发送事件](sending-an-event-with-wmifireevent.md)。

 

 




