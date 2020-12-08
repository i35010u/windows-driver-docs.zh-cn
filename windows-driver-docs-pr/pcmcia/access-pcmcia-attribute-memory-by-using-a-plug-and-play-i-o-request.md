---
title: 使用 PnP i/o 请求访问内存
description: 使用即插即用 I/O 请求访问 PCMCIA 属性内存
keywords:
- 属性内存 WDK PCMCIA 总线，即插即用 i/o 请求
- 即插即用 WDK PCMCIA 总线
- PnP WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77409df372524b0b2e9c8408977e9c28fb2b633c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812519"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-plug-and-play-io-request"></a>使用即插即用 I/O 请求访问 PCMCIA 属性内存





本部分介绍 PC 卡或 Cardbus 卡驱动程序如何使用即插即用 i/o 请求来访问属性内存。

驱动程序通常使用此方法来初始化设备、配置设备或从设备获取信息。 如果 i/o 开销是可接受的，则驱动程序应使用此方法，并且可以在 IRQL &lt; 调度级别进行访问 \_ 。

在以 IRQL 调度级别运行时，驱动程序只能使用此方法 &lt; \_ 。

驱动程序执行以下一系列操作：

-   创建并初始化新的 IRP \_ MJ \_ PNP 请求。

    驱动程序指定 [**irp \_ MN \_ READ \_ config**](../kernel/irp-mn-read-config.md) 或 [**irp \_ MN \_ WRITE \_ config**](../kernel/irp-mn-write-config.md) 次要函数。

-   获取下一个堆栈位置。

-   设置新堆栈位置的 **ReadWriteConfig** 结构的以下成员：

    <a href="" id="whichspace"></a>**WhichSpace**  
    指定值 PCCARD \_ 属性 \_ 内存。

    <a href="" id="buffer"></a>**宽限**  
    指向驱动程序为访问分配的分页内存缓冲区的指针。 对于写入操作，缓冲区包含要写入配置空间的数据。 对于读取操作，该缓冲区是一个填充了零的缓冲区。 请求完成后，此缓冲区保存从设备读取的属性内存副本。

    <a href="" id="offset"></a>**抵销**  
    指定从读取或写入操作开始的属性内存基数开始的单词偏移量。

    <a href="" id="length"></a>**长短**  
    指定驱动程序为请求分配的缓冲区的大小（以字节为单位）。

-   设置完成例程。

-   按设备堆栈向下发送请求。

 

