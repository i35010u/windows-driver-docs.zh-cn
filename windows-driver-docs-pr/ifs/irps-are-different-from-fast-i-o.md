---
title: IRP 不同于快速 I/O
description: IRP 不同于快速 I/O
keywords:
- Irp WDK 文件系统
- fast i/o 与 Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f65b43ed22c62b29fb7e51f41774b630dea77297
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819055"
---
# <a name="irps-are-different-from-fast-io"></a>IRP 不同于快速 I/O


## <span id="ddk_irps_are_different_from_fast_io_if"></span><span id="DDK_IRPS_ARE_DIFFERENT_FROM_FAST_IO_IF"></span>


Irp 是用于请求 i/o 操作的默认机制。 Irp 可用于同步或异步 i/o，适用于缓存或非缓存 i/o。 Irp 还用于分页 i/o。 内存管理器通过将相应的 Irp 发送到文件系统来处理页错误。

Fast i/o 专门设计用于缓存文件中的快速同步 i/o。 在快速 i/o 操作中，数据直接在用户缓冲区和系统缓存之间传输，绕过文件系统和存储驱动程序堆栈。  (存储驱动程序不使用 fast i/o。 ) 如果在收到快速 i/o 读取或写入请求时，从文件中读取的所有数据都在系统缓存中，则会立即满足请求。 否则，可能会出现页错误，导致生成一个或多个 Irp。 发生这种情况时，快速 i/o 例程要么返回 **FALSE**，要么将调用方置于等待状态，直到处理页错误。 如果快速 i/o 例程返回 **FALSE**，则请求的操作失败，并且调用方必须创建 IRP。

支持 Irp 需要文件系统和文件系统筛选器，但不需要支持快速 i/o。 但是，文件系统和文件系统筛选器必须实现快速 i/o 例程。 即使文件系统和文件系统筛选器不支持快速 i/o，它们也必须定义一个返回 **FALSE** (的快速 i/o 例程，即快速 i/o 例程不会实现任何功能) 。 当 i/o 管理器接收到 (对分页 i/o) 以外的同步文件 i/o 的请求时，将首先调用 fast i/o 例程。 如果快速 i/o 例程返回 **TRUE**，则该操作由快速 i/o 例程提供服务。 如果快速 i/o 例程返回 **FALSE**，则 I/o 管理器将改为创建并发送 IRP。

文件系统筛选器驱动程序不需要支持控制设备对象上的 i/o。 但是，需要对附加到文件系统或卷的筛选设备对象将所有无法识别或不需要的 Irp 传递到驱动程序堆栈上的下一个较低版本的驱动程序。 此外，附加到卷的筛选设备对象必须实现 FastIoDetachDevice。

 

 




