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
ms.openlocfilehash: c256fea79a7ac7ee28d7771654a72714edd065aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835685"
---
# <a name="wmi-event-tracing"></a>WMI 事件跟踪





本部分介绍了作为信息提供商提供的信息提供商提供的信息，这是内核模式驱动程序（Windows 2000 及更高版本支持）的 WMI 扩展。 驱动程序通常提供使用者用于确定驱动程序的配置和资源使用情况的信息。 除了对 WDM 的 WMI 扩展外，用户模式 API 还支持 WMI 事件信息的提供者或使用者-有关详细信息，请参阅 Windows SDK。

事件跟踪记录器最多支持32实例。 其中一个实例保留用于跟踪内核。 记录器支持跟踪高事件率。

跟踪事件的定义方式与其他 WMI 事件的定义方式相同。 MOF 文件中介绍了 WMI 事件。 有关 WMI 事件描述的详细信息，请参阅[Wmi 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)。

内核模式驱动程序日志信息集成到现有 WMI 基础结构中所使用的过程。 若要记录跟踪事件，驱动程序需要执行以下操作：

1.  通过调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)注册为 WMI 提供程序。

2.  将事件标记为可[**跟踪，方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)是在驱动程序向 WMI 注册事件时，通过将 WMIREG\_标志设置\_跟踪\_GUID 的**标志**成员中。

3.  将一个事件指定为控制事件，以便对一组跟踪事件进行整体启用/禁用，方法是将\_\_\_WMIREG 设置为在**WMIREGGUID**结构的**Flags**成员中\_GUID驱动程序向 WMI 注册事件。

4.  接收到 WMI 的请求以启用 GUID 与跟踪控制 GUID 匹配的事件时，驱动程序应将句柄存储在记录器中。 写入事件时将需要该值。 有关如何使用此句柄的信息，请参阅步骤6。 记录器句柄值包含在作为 enable events 请求中的参数的一部分的 WMI 缓冲区的[**WNODE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)部分的**HistoricalContext**成员中。

5.  确定跟踪事件是发送到 WMI 事件使用者还是仅针对 WMI 事件记录器。 这将确定[**事件\_跟踪\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff544329)结构应来自的内存。 此内存最终会传递到[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)。

    如果事件仅为日志事件，则 WMI 不会删除内存。 在这种情况下，驱动程序应传入堆栈上的缓冲区，或者出于此目的应重用已分配的缓冲区。 出于性能原因，驱动程序应最大程度地减少分配或释放内存的任何不必要的调用。 如果未遵守此建议，将会损害日志文件中包含的计时信息的完整性。

    如果要将事件同时发送到记录器和 WMI 事件使用者，则必须从非分页池分配内存。 在这种情况下，会将事件发送到记录器，然后将其转发到 WMI，以发送到已请求事件通知的 WMI 事件使用者。 然后，WMI 会根据**IoWMIWriteEvent**的行为释放该事件的内存。

6.  在事件的内存[ **\_TRACE\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff544329)和任何驱动程序事件数据（如果有）受到保护后，应设置以下信息：

    将**size**成员设置为 Sizeof （**事件\_TRACE\_标头**）加上附加的任何驱动程序事件数据的大小，该数据将追加到**事件结束\_TRACE\_标头**。

    将**Flags**成员设置为 WNODE\_标记\_跟踪\_GUID，以将事件发送到记录器。 如果还将事件发送到 WMI 事件使用者，请将 WNODE\_标志设置\_LOG\_WNODE。 请注意，如果将 WNODE\_标记设置\_日志\_WNODE，则不需要设置 WNODE\_标志\_跟踪\_GUID。 如果同时设置了这两个\_标志，则\_跟踪\_GUID 将优先，并且不会将事件发送到 WMI 事件使用者。

    设置**Guid**或**GuidPtr**成员。 如果使用**GuidPtr**，请将 WNODE\_标志设置\_在**FLAGS**成员中使用\_GUID\_PTR。

    还可以指定**时间戳**的值。 如果驱动程序未指定**时间戳**值，则记录器将在中填充此值。 如果驱动程序不希望记录器设置时间戳，则应将 WNODE\_标志设置\_在**Flags**成员中使用\_时间戳。

    设置以下任何**事件\_跟踪**对驱动程序有意义的\_标头成员：**类**、类、**类**和**类**。

    最后，将**事件\_TRACE\_标头**强制转换为**WNODE\_标头**，并将**WNODE**的**HistoricalContext**值设置为上面步骤4中保存的记录器句柄。

7.  调用[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent) ，将指针与指向**事件\_TRACE\_标头**结构。

驱动程序应继续记录与控件 GUID 关联的跟踪事件，直到驱动程序收到通知，以便通过**IRP\_MN\_禁用\_事件**请求来禁用事件日志记录。

 

 




