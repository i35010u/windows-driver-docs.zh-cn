---
title: 读取和写入属性内存
description: 读取和写入属性内存
ms.assetid: 8e430057-b68a-4edc-8755-1d7255412269
keywords:
- PCMCIA WDK 总线，属性内存
- WDK PCMCIA 总线内存、 读取和写入属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd15a15d86a294fe2a2cd511f2b615ec96218522
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575869"
---
# <a name="read-and-write-attribute-memory"></a>读取和写入属性内存





本部分介绍如何 PCMCIA 驱动程序可以读写属性内存 PCMCIA 内存卡上。

Windows 2000 和更高版本操作系统视为属性内存 PC 卡或 CardBus 卡上配置空间。

一般情况下，若要访问属性的内存，驱动程序上必须要创建使用主要函数代码的 IRP IRP\_MJ\_PNP 和次要函数代码[ **IRP\_MN\_读取\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)或[ **IRP\_MN\_编写\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551769)。

如有必要，驱动程序可以直接通过永久内存窗口访问属性内存。 请参阅[访问 PCMCIA 属性内存通过永久内存窗口](https://msdn.microsoft.com/library/windows/hardware/ff536901)的更多详细信息。

PCMCIA 内存卡驱动程序将执行以下操作：

-   创建并初始化新的 IRP。

-   获取下一步的堆栈位置。

-   设置新的堆栈位置的以下成员：
    -   **ReadWriteConfig.WhichSpace**成员指定值 PCCARD\_属性\_内存。
    -   **缓冲区**成员将指向驱动程序分配，非分页缓冲区的读取或写入操作。 写入操作，该缓冲区包含要写入到配置区域的数据。 对于读取操作，缓冲区是零填充缓冲区。 IRP 完成后，此缓冲区设置为从设备读取的属性内存的副本。
    -   **偏移量**成员指定的字节偏移量属性内存读取或写入操作的开始位置的基。
    -   **长度**成员指定的大小，以字节为单位，在指定的缓冲区**缓冲区**。
-   设置完成例程。

-   将驱动器在堆栈的下层请求发送。

驱动程序必须运行在 IRQL&lt;调度\_要发送此请求关闭驱动程序堆栈级别。

 

 





