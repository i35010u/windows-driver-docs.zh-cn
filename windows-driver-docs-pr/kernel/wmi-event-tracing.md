---
title: WMI 事件跟踪
description: WMI 事件跟踪
ms.assetid: 72505a9a-830a-4529-ba73-31af0fedfeec
keywords:
- WMI WDK 内核，事件跟踪
- 事件 WDK WMI
- 跟踪 WDK WMI
- WMI WDK 内核，WDM 驱动程序
- WDM 驱动程序 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1b11d536af0ef5ad6ec54edf0f5086dcdfd2aa8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184097"
---
# <a name="wmi-event-tracing"></a>WMI 事件跟踪





本部分介绍了 Windows 2000 和更高版本支持的对 WDM (的 WMI 扩展) 该内核模式驱动程序（如信息提供程序）可用于向信息使用者提供信息。 驱动程序通常提供使用者用于确定驱动程序的配置和资源使用情况的信息。 除了对 WDM 的 WMI 扩展外，用户模式 API 还支持 WMI 事件信息的提供者或使用者-有关详细信息，请参阅 Windows SDK。

事件跟踪记录器最多支持32实例。 其中一个实例保留用于跟踪内核。 记录器支持跟踪高事件率。

跟踪事件的定义方式与其他 WMI 事件的定义方式相同。 MOF 文件中介绍了 WMI 事件。 有关 WMI 事件描述的详细信息，请参阅 [Wmi 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)。

内核模式驱动程序日志信息集成到现有 WMI 基础结构中所使用的过程。 若要记录跟踪事件，驱动程序需要执行以下操作：

1.  通过调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)注册为 WMI 提供程序。

2.  通过在 \_ \_ \_ 驱动程序向 WMI 注册事件时传递的[**WMIREGGUID**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)结构的**Flags**成员中设置 WMIREG 标志跟踪 GUID，将事件标记为可跟踪。

3.  指定一个事件作为控制事件，以便对一组跟踪事件进行整体启用/禁用，方法 \_ \_ \_ \_ 是在驱动程序向 WMI 注册事件时传递的**WMIREGGUID**结构的**Flags**成员中设置 WMIREG 标志跟踪控制 GUID。

4.  接收到 WMI 的请求以启用 GUID 与跟踪控制 GUID 匹配的事件时，驱动程序应将句柄存储在记录器中。 写入事件时将需要该值。 有关如何使用此句柄的信息，请参阅步骤6。 记录器句柄值包含在作为 enable events 请求中的参数的一部分的 WMI 缓冲区的[**WNODE \_ 标头**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)部分的**HistoricalContext**成员中。

5.  确定跟踪事件是发送到 WMI 事件使用者还是仅针对 WMI 事件记录器。 这将确定 [**事件 \_ 跟踪 \_ 标头**](/previous-versions/ff544329(v=vs.85)) 结构的内存应来自何处。 此内存最终会传递到 [**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)。

    如果事件仅为日志事件，则 WMI 不会删除内存。 在这种情况下，驱动程序应传入堆栈上的缓冲区，或者出于此目的应重用已分配的缓冲区。 出于性能原因，驱动程序应最大程度地减少分配或释放内存的任何不必要的调用。 如果未遵守此建议，将会损害日志文件中包含的计时信息的完整性。

    如果要将事件同时发送到记录器和 WMI 事件使用者，则必须从非分页池分配内存。 在这种情况下，会将事件发送到记录器，然后将其转发到 WMI，以发送到已请求事件通知的 WMI 事件使用者。 然后，WMI 会根据 **IoWMIWriteEvent**的行为释放该事件的内存。

6.  在 [**事件 \_ 跟踪 \_ 标头**](/previous-versions/ff544329(v=vs.85)) 的内存和任何驱动程序事件数据（如果有）受到保护之后，应设置以下信息：

    将 **size** 成员设置为 Sizeof (**事件 \_ 跟踪 \_ 标头**) 加上附加到 **事件 \_ 跟踪 \_ 标头**末尾的任何其他驱动程序事件数据的大小。

    将 **Flags** 成员设置为 WNODE \_ 标志 \_ 跟踪 \_ GUID，以将事件发送到记录器。 如果事件也将发送到 WMI 事件使用者，请设置 WNODE \_ 标志 \_ LOG \_ WNODE。 请注意， \_ \_ \_ 如果设置 WNODE \_ 标记 \_ 日志 \_ WNODE，则不需要设置 WNODE 标志跟踪 GUID。 如果同时设置了这两个，则 \_ 将优先使用 WNODE 标志 \_ 跟踪 \_ GUID，并且不会将事件发送到 WMI 事件使用者。

    设置 **Guid** 或 **GuidPtr** 成员。 如果使用 **GuidPtr**，请 \_ \_ \_ \_ 在 **Flags** 成员中设置 WNODE 标志使用 GUID PTR。

    还可以指定 **时间戳**的值。 如果驱动程序未指定 **时间戳** 值，则记录器将在中填充此值。 如果驱动程序不希望记录器设置时间戳，则应 \_ \_ 在 Flags 成员中设置 WNODE 标志使用 \_ 时间戳。 **Flags**

    设置以下任何对驱动程序有意义的 **事件 \_ 跟踪 \_ 标头** 成员： **类**、类、 **类**和 **类**。

    最后，将**事件 \_ 跟踪 \_ 标头**强制转换为**WNODE \_ 标头**，并将**WNODE**的**HistoricalContext**值设置为上面步骤4中保存的记录器句柄。

7.  调用 [**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent) ，并将指针指向 **事件 \_ 跟踪 \_ 标头** 结构。

驱动程序应继续记录与控件 GUID 关联的跟踪事件，直到驱动程序收到通知，以通过 **IRP \_ MN \_ disable \_ events** 请求来禁用事件日志记录。

 

