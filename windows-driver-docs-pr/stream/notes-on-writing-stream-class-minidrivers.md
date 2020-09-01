---
title: 有关如何编写流类微型驱动程序的说明
description: 有关如何编写流类微型驱动程序的说明
ms.assetid: dc966b47-4ffe-4122-847d-118a465bf5f5
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，写入
- 流式处理微型驱动程序 WDK Windows 2000 内核，写入
- 微型驱动程序 WDK Windows 2000 内核流式处理，写入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cbd2c4967848d082cc5d4ab1918373796eed3ff
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192143"
---
# <a name="notes-on-writing-stream-class-minidrivers"></a>有关如何编写流类微型驱动程序的说明





-   微型驱动程序必须在 Intel 和非 Intel x86 处理器上运行，因此必须以 C (或其他高级语言) 编写。 微型驱动程序不应包含程序集语言源代码。

-   某些硬件在运行之前需要加载固件。 微型驱动程序应在微型驱动程序的数据段中嵌入固件。 微型驱动程序可以根据需要通过调用相应的 WDM 文件 i/o 函数动态加载其固件，例如，微型驱动程序使用几个固件版本，这些版本将导致嵌入不现实。

-   通过将[**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)结构中的**TurnOffSynchronization**成员设置为**TRUE** ，关闭同步 () 如果微型驱动程序需要转到被动 \_ 级别 (适用于大多数请求的低优先级) 。 有关同步的详细信息，请参阅 [微型驱动程序同步](minidriver-synchronization.md) 部分。

-    (端口或内存地址) 的硬件资源应该通过在 *wdm*中找到的宏进行访问。 例如，若要写入 word 端口， \_ 应使用宏写入端口 \_ USHORT。 若要将缓冲区写入端口， \_ \_ 应使用写入端口缓冲区 \_ USHORT。

-   微型驱动程序不应具有未受保护的自旋循环。 如果在等待端口值更改时微型驱动程序需要进行旋转，则循环必须由循环计数器保护。

-   需要以同步方式等待一小段时间的微型驱动程序应使用 [**KeStallExecutionProcessor**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor)。 应慎用此例程，以便不会降低系统性能。

-   需要等待很长一段)  (时间才能完成操作的微型驱动程序，必须是中断驱动的，或者使用 [**StreamClassScheduleTimer**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassscheduletimer) 函数来计划定时回调。 微型驱动程序不应旋转等待状态更改的几个微秒，因为这会降低系统的整体性能。

-   使用总线主控 DMA 的设备只需使用流请求块结构中提供的散播/聚集 DMA 列表， ([**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)) 。 不需要锁定或映射 DMA 缓冲区。 有关详细信息，请参阅 **HW \_ 流 \_ 请求 \_ 块** 结构。 此外，如果微型驱动程序需要中断 DMA 请求，则可以使用 [**StreamClassGetPhysicalAddress**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassgetphysicaladdress) 函数获取虚拟缓冲区指针内的偏移量的物理地址。

 

