---
title: IRP 不同于快速 I/O
description: IRP 不同于快速 I/O
ms.assetid: 22b08da2-043e-4724-b8f1-90b337fa222c
keywords:
- Irp WDK 文件系统
- 快速 I/O vs。Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdadd91334ed4dd2f75a1e1aa90c978b85787bf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324258"
---
# <a name="irps-are-different-from-fast-io"></a>IRP 不同于快速 I/O


## <span id="ddk_irps_are_different_from_fast_io_if"></span><span id="DDK_IRPS_ARE_DIFFERENT_FROM_FAST_IO_IF"></span>


Irp 是请求 I/O 操作的默认机制。 可以使用 Irp，以便执行同步或异步 I/O，并针对缓存或非缓存的 I/O。 Irp 还用于分页 I/O。 内存管理器进程通过将相应的 Irp 发送到文件系统的页错误。

快速 I/O 专为快速同步 I/O 上缓存的文件。 在快速 I/O 操作中，数据传输之间用户缓冲区和系统缓存中，直接跳过文件系统和存储驱动程序堆栈。 （存储驱动程序不使用快速 I/O。）如果要从文件读取的数据都驻留在系统缓存中时快速 I/O 读取或写入收到请求时，立即满足请求。 否则，会发生页面错误，导致一个或多个 Irp 生成。 当发生这种情况，快速 I/O 例程返回**FALSE**，或使调用方进入等待状态，直到处理页面错误。 如果快速 I/O 例程将返回**FALSE**、 请求的操作失败和调用方必须创建 IRP。

支持 Irp，所需的文件系统和文件系统筛选器，但不是需要它们以支持快速 I/O。 但是，文件系统和文件系统筛选器必须实现快速 I/O 例程。 即使文件系统和文件系统筛选器不支持快速 I/O，它们必须定义返回的快速 I/O 例程**FALSE** （即，快速 I/O 例程不实现任何功能）。 当 I/O 管理器收到的 （而不是分页 I/O) 的同步文件 I/O 请求时，它首先调用快速 I/O 例程。 如果快速 I/O 例程将返回 **，则返回 TRUE**，该操作已由快速 I/O 例程提供服务。 如果快速 I/O 例程将返回**FALSE**，I/O 管理器创建并改为发送 IRP。

文件系统筛选器驱动程序不支持所需 I/O 上控制设备对象。 但是，筛选设备对象附加到文件系统或卷所需将所有无法识别或不需要的 Irp 传递给下一步低驱动程序，驱动程序堆栈上。 此外，附加到卷的筛选设备对象必须实现 FastIoDetachDevice。

 

 




