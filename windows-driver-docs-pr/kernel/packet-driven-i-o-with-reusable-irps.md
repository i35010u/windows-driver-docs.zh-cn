---
title: 数据包驱动的 I/O 与可重用 IRP
description: 数据包驱动的 I/O 与可重用 IRP
keywords:
- I/o 堆栈位置 WDK 内核
- 数据包驱动 i/o WDK 内核
- 重用 Irp WDK 内核
- 标头 WDK 内核
- I/o 管理器通信 WDK 内核
- I/o 状态阻止 WDK 内核
- 状态阻止 WDK 内核
- 堆栈位置 WDK 内核
- Irp WDK 内核，重复使用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39405c6553040195a4858b89430ec7c34a1431ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837215"
---
# <a name="packet-driven-io-with-reusable-irps"></a>数据包驱动的 I/O 与可重用 IRP





I/o 管理器、即插即用 manager 和电源管理器使用 *i/o 请求包* (irp) 与内核模式驱动程序通信，并允许驱动程序彼此通信。

I/o 管理器执行以下步骤：

-   接受 i/o 请求，这些请求通常源自用户模式应用程序。

-   创建 Irp 来表示 i/o 请求。

-   将 Irp 路由到适当的驱动程序。

-   跟踪 Irp，直到完成。

-   将状态返回给每个 i/o 操作的原始请求者。

IRP 可能会路由到多个驱动程序。 例如，在磁盘上打开文件的请求可能首先进入文件系统驱动程序、通过中间镜像驱动程序，并最终到达磁盘驱动程序，也可能是 PnP 硬件总线驱动程序。 这组驱动程序称为 *驱动程序堆栈*。

因此，每个 IRP 都有一个 *固定部分*，并为每个控制设备的驱动程序提供一个特定于驱动程序的 *i/o 堆栈位置* ：

-   在固定部分 (或 *标头*) ，i/o 管理器将维护有关原始请求的信息，例如调用方的线程 ID 和参数、打开文件的设备对象的地址等。 固定部分还包含一个 *i/o 状态块*，其中，驱动程序设置有关请求的 i/o 操作状态的信息。

-   在最高层驱动程序的 i/o 堆栈位置，i/o 管理器、即插即用 manager 或电源管理器设置特定于驱动程序的参数，例如请求的操作的函数代码和相应的驱动程序用来确定应执行的操作的上下文。 反过来，每个驱动程序会在驱动程序堆栈中设置下一个较低驱动程序的 i/o 堆栈位置。

由于每个驱动程序都处理 IRP，因此它可以在 IRP 中访问其 i/o 堆栈位置，从而在驱动程序操作的每个阶段重复使用 IRP。 此外，更高级别的驱动程序可以创建 (或重复使用) Irp 将请求发送到更低级别的驱动程序。

有关 Irp 的详细讨论，请参阅 [处理 irp](handling-irps.md)。

 

 




