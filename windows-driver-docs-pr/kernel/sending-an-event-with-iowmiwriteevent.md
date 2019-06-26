---
title: 使用 IoWMIWriteEvent 发送事件
description: 使用 IoWMIWriteEvent 发送事件
ms.assetid: 77c1041a-340c-4c59-a30a-e946adf60a95
keywords:
- WMI WDK 内核事件跟踪
- WDK WMI 事件
- 跟踪 WDK WMI
- 发送的 WMI 事件
- 事件阻止 WDK WMI
- 通知 WDK WMI
- IoWMIWriteEvent
- 动态实例名称 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e92bf58dcfefcebfaeb3b863bb2a09354fddaf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364083"
---
# <a name="sending-an-event-with-iowmiwriteevent"></a>使用 IoWMIWriteEvent 发送事件





驱动程序可以调用[ **IoWMIWriteEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiwriteevent)发送任何事件。 事件可以包含单个项、 单个实例或所有实例的数据块，并且它可以使用动态实例名称。

与不同**WNODE\_* XXX*** 查询或更改请求，它将分配和部分初始化由 WMI，与传递的结构驱动程序必须分配并初始化的所有成员**WNODE\_* XXX*** 结构，其中包含一个事件。

驱动程序必须发送事件才发送 WMI [ **IRP\_MN\_启用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)请求以启用该事件。 然后，发生事件的触发器条件时，该驱动程序：

1. 分配非分页缓冲池包含从缓冲区**WNODE\_* XXX*** 事件，包括变量的数据的空间，如果任何所需的结构。

   根据事件，该驱动程序可能会分配[ **WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)即[ **WNODE\_单\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)，或[ **WNODE\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_all_data)事件。 大小**WNODE\_* XXX*** 以及变量的数据不能超过 1 K 的注册表定义的限制。

2. 初始化的所有成员**WNODE\_* XXX*** 结构，包括**WnodeHeader.Flags**:

   - 驱动程序集**WNODE\_标志\_事件\_项**标志，用于指示结构是一种事件。

   - 驱动程序设置以下标志来指示的类型之一**WNODE\_* XXX*** 结构：

     **WNODE\_FLAG\_ALL\_DATA**

     **WNODE\_FLAG\_SINGLE\_INSTANCE**

     **WNODE\_FLAG\_SINGLE\_ITEM**

   - 该驱动程序设置或清除以下标志以指示块是否使用静态或动态实例名称：

     **WNODE\_FLAG\_STATIC\_INSTANCE\_NAMES**

     **WNODE\_FLAG\_PDO\_INSTANCE\_NAMES**

   - 该驱动程序可能会设置其他标志，具体取决于该事件。

3. 将指向的指针强制转换**WNODE\_* XXX*** 到 PWNODE\_事件\_项。

4. 调用**IoWMIWriteEvent**的指针。

   如果**IoWMIWriteEvent**成功完成后，该事件的 WMI 版本驱动程序分配内存。

之后[ **IoWMIWriteEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiwriteevent)返回时，该驱动程序将恢复监视事件的触发条件和发送事件及其触发条件发生，直到发送了 WMI 每次[ **IRP\_MN\_禁用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)禁用该事件的请求。

如果事件的大小超过了注册表定义最大 1 K （不推荐） 的驱动程序应调用**IoWmiWriteEvent**具有初始化[ **WNODE\_事件\_引用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_event_reference) ，它指定事件的 GUID，其大小及其 （适用于静态实例名称） 的实例索引或名称 （对于动态实例名称）。 WMI 将使用中的信息**WNODE\_事件\_引用**到事件查询。

驱动程序可以发送事件，不使用动态实例名称和其中包含单个实例通过调用 WMI 库例程[ **WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmifireevent)。 该驱动程序不需要分配并初始化**WNODE\_* XXX*** 结构**WmiFireEvent**调用。 WMI 包中的驱动程序的事件数据[ **WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)将其传递到数据使用者。 有关发送事件的详细信息**WmiFireEvent**，请参阅[发送与 WmiFireEvent 事件](sending-an-event-with-wmifireevent.md)。

 

 




