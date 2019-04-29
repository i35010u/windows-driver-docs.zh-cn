---
title: WMI 事件跟踪
description: WMI 事件跟踪
ms.assetid: 72505a9a-830a-4529-ba73-31af0fedfeec
keywords:
- WMI WDK 内核事件跟踪
- WDK WMI 事件
- 跟踪 WDK WMI
- WMI WDK 内核，WDM 驱动程序
- WDM 驱动程序 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdf10164a3358c49d7d9f4e0675407afd5770cbc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393012"
---
# <a name="wmi-event-tracing"></a>WMI 事件跟踪





本部分介绍的内核模式驱动程序，为信息提供者的 WDM （由 Windows 2000 及更高版本支持） 的 WMI 扩展，可用于提供信息到信息使用者。 驱动程序通常提供使用者用来确定驱动程序的配置和资源使用情况信息。 除了 WDM 的 WMI 扩展，用户模式 API 还支持提供程序或使用者的 WMI 事件的信息，请参阅 Windows SDK 的详细信息。

事件跟踪记录器支持最多 32 个实例。 用于跟踪内核保留其中一个实例。 记录器支持跟踪高事件速率。

跟踪事件中与其他 WMI 事件相同的方式定义。 MOF 文件中描述了 WMI 事件。 WMI 事件说明的详细信息，请参阅[WMI 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)。

按其内核模式驱动程序记录信息的过程集成到现有的 WMI 基础结构。 若要记录跟踪事件，驱动程序执行以下任务：

1.  将注册为 WMI 提供程序通过调用[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)。

2.  将作为可跟踪的事件标记通过设置 WMIREG\_标志\_跟踪\_中的 GUID**标志**隶属[ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)当驱动程序通过 WMI 注册事件时传递的结构。

3.  指定作为整体启用/禁用的一组跟踪事件的控件事件一个事件，通过设置 WMIREG\_标志\_跟踪\_控件\_中的 GUID**标志**的成员**WMIREGGUID**时驱动程序向 WMI 注册事件传递的结构。

4.  收到请求后从 WMI 启用 GUID 与跟踪控件的 GUID 相匹配的事件，该驱动程序应将存储到记录器的句柄。 编写一个事件时，将需要该值。 有关如何使用此句柄的信息，请参阅步骤 6。 记录器句柄值包含在**HistoricalContext**的成员[ **WNODE\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566375)是参数的一部分的 WMI 缓冲区的一部分在启用事件请求。

5.  确定是否跟踪事件将发送到 WMI 事件使用者，还是针对 WMI 事件记录器。 这将确定位置的内存[**事件\_跟踪\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff544329)结构应该来自于。 此内存将最终传递给[ **IoWMIWriteEvent**](https://msdn.microsoft.com/library/windows/hardware/ff550520)。

    如果该事件是一个日志事件，则内存不会删除由 WMI 中。 在这种情况下，该驱动程序应在堆栈上传递的缓冲区中，或应为实现此目的重复使用的分配的缓冲区。 出于性能原因，该驱动程序应最小化任何不必要的调用来分配或释放内存。 不符合此建议将破坏日志文件中包含的计时信息的完整性。

    如果该事件将发送到这两个记录器和 WMI 事件使用者，然后必须从非分页缓冲池分配内存。 在这种情况下将发送到记录器，然后转发到 WMI，以发送到 WMI 事件使用者已请求事件通知的事件。 根据的行为则由 WMI 释放事件内存**IoWMIWriteEvent**。

6.  之后的内存[**事件\_跟踪\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff544329)和任何驱动程序的事件数据，如果有，都已得到保护，应设置以下信息：

    设置**大小**成员与 sizeof (**事件\_跟踪\_标头**) 的任何其他驱动程序事件数据将追加到末尾的大小以及**事件\_跟踪\_标头**。

    设置**标志**成员添加到 WNODE\_标志\_跟踪\_GUID 具有发送到记录器的事件。 如果该事件将发送到 WMI 事件接收器，设置 WNODE\_标志\_日志\_WNODE。 请注意，不需要设置 WNODE\_标志\_跟踪\_GUID 如果设置 WNODE\_标志\_日志\_WNODE。 如果两者都设置的 WNODE\_标志\_跟踪\_GUID 优先，事件将不发送到 WMI 事件使用者。

    设置**Guid**或**GuidPtr**成员。 如果使用**GuidPtr**，设置 WNODE\_标志\_使用\_GUID\_中的 PTR**标志**成员。

    （可选） 指定的值**时间戳**。 如果未指定驱动程序**时间戳**值记录器将填充此。 如果该驱动程序不想要设置的时间戳的记录器，则它应设置 WNODE\_标志\_使用\_中的时间戳**标志**成员。

    设置任何以下**事件\_跟踪\_标头**对驱动程序有含义的成员：**Class.Type**， **Class.Level**，和**Class.Version**。

    最后强制转换**事件\_跟踪\_标头**到**WNODE\_标头**并设置**HistoricalContext** 值**Wnode**到记录器句柄时保存在上述步骤 4。

7.  调用[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)用指针指向**事件\_跟踪\_标头**结构。

该驱动程序应继续日志记录与控件 GUID，直到该驱动程序收到通知，以禁用通过事件日志记录的跟踪事件**IRP\_MN\_禁用\_事件**请求。

 

 




