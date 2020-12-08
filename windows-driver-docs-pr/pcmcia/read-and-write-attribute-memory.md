---
title: 读取和写入属性内存
description: 读取和写入属性内存
keywords:
- PCMCIA WDK 总线，属性内存
- 属性内存 WDK PCMCIA 总线，读取和写入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1c3184dea14dcd95edc77c9263cf6a12ca5c831
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806049"
---
# <a name="read-and-write-attribute-memory"></a>读取和写入属性内存





本部分介绍 PCMCIA 驱动程序如何读取和写入 PCMCIA 内存卡上的属性内存。

Windows 2000 和更高版本的操作系统将 PC 卡或 CardBus 卡上的属性内存视为配置空间。

通常，若要访问属性内存，驱动程序必须使用 IRP MJ PNP 的主要功能代码 \_ \_ 和 [**irp \_ MN \_ READ \_ config**](../kernel/irp-mn-read-config.md) 或 [**irp \_ MN \_ 写入 \_ 配置**](../kernel/irp-mn-write-config.md)的次要函数代码创建 IRP。

如有必要，驱动程序可以通过永久性内存窗口直接访问属性内存。 有关更多详细信息，请参阅 [通过永久性内存窗口访问 PCMCIA 属性内存](./access-pcmcia-attribute-memory-through-a-permanent-memory-window.md) 。

PCMCIA 内存卡驱动程序执行以下操作：

-   创建并初始化新的 IRP。

-   获取下一个堆栈位置。

-   设置新堆栈位置的以下成员：
    -   **ReadWriteConfig. WhichSpace** 成员指定值 PCCARD \_ 属性 \_ 内存。
    -   **缓冲区** 成员指向用于读取或写入操作的驱动程序分配的非分页缓冲区。 对于写入操作，缓冲区包含要写入配置空间的数据。 对于读取操作，该缓冲区是一个填充了零的缓冲区。 完成 IRP 后，此缓冲区设置为从设备读取的属性内存副本。
    -   **Offset** 成员指定从属性内存基开始读取或写入操作的字节偏移量。
    -   **Length** 成员指定 **缓冲区** 中指定的缓冲区的大小（以字节为单位）。
-   设置完成例程。

-   沿驱动器堆栈向下发送请求。

驱动程序必须以 IRQL &lt; 调度级别运行 \_ ，才能将此请求沿驱动程序堆栈向下发送。

 

