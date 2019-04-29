---
title: 有关如何编写流类微型驱动程序的说明
description: 有关如何编写流类微型驱动程序的说明
ms.assetid: dc966b47-4ffe-4122-847d-118a465bf5f5
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核、 编写
- 流式处理微型驱动程序 WDK Windows 2000 内核、 编写
- 微型驱动程序 WDK Windows 2000 内核流式处理、 编写
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1d98a59d1a7ec0d56f592433abaace309990f38
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377765"
---
# <a name="notes-on-writing-stream-class-minidrivers"></a>有关如何编写流类微型驱动程序的说明





-   微型驱动程序必须运行 Intel 和非 Intel x86 处理器，并因此必须用 C （或其他高级语言） 编写。 微型驱动程序不应包含程序集语言的源代码。

-   某些硬件所需固件必须先将正常加载。 微型驱动程序应嵌入微型驱动程序的数据段中的固件。 （可选） 微型驱动程序可以动态加载其固件通过调用适当的 WDM 文件 I/O 函数，如果，例如，微型驱动程序使用多个版本的固件可能会使嵌入不切实际。

-   关闭同步 (通过设置**TurnOffSynchronization**中的成员[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682) 结构**TRUE**) 如果微型驱动程序需要转到被动\_请求最多的级别 （优先级较低）。 请参阅[微型驱动程序同步](minidriver-synchronization.md)部分，了解有关同步的详细信息。

-   硬件资源 （端口或内存地址） 应通过在中找到的宏访问*wdm.h 中*。 例如，若要写入到 word 端口，该宏编写\_端口\_应使用 USHORT。 若要写入端口的缓冲区，编写\_端口\_缓冲区\_应使用 USHORT。

-   微型驱动程序应不具有不受保护数值调节钮循环。 如果微型驱动程序需要的旋转等待的一个端口，以更改值时，必须通过循环计数器保护循环。

-   需要同步等待一小段时间应使用的微型驱动程序[ **KeStallExecutionProcessor**](https://msdn.microsoft.com/library/windows/hardware/ff553295)。 因此不会降低系统性能，应谨慎使用此例程。

-   需要等待一段很长的时间 （超过几微秒） 的某个操作完成的微型驱动程序应是中断驱动，或使用[ **StreamClassScheduleTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff568264)函数计划的定时的回调。 微型驱动程序应等待状态的变化，因为它会降低整体系统性能的多个几微秒的旋转。

-   使用总线 master DMA 的设备只需使用提供的流请求块结构中的分散/聚拢 DMA 列表 ([**HW\_流\_请求\_块**](https://msdn.microsoft.com/library/windows/hardware/ff559702)). 没有锁定或 DMA 缓冲区映射是必需的。 请参阅**HW\_流\_请求\_阻止**结构的详细信息。 此外，如果需要分解为多 DMA 请求微型驱动程序[ **StreamClassGetPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff568247)函数可用于获取中的虚拟缓冲区指针的偏移量的物理地址。

 

 




