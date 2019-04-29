---
title: 数据包驱动的 I/O 与可重用 IRP
description: 数据包驱动的 I/O 与可重用 IRP
ms.assetid: ff315b61-9fa3-4a20-bc3e-82db0ea3cde7
keywords:
- I/O 堆栈位置 WDK 内核
- 数据包驱动 I/O WDK 内核
- 重复使用 Irp WDK 内核
- 标头 WDK 内核
- I/O 管理器通信 WDK 内核
- I/O 状态块 WDK 内核
- 状态块 WDK 内核
- 堆栈位置 WDK 内核
- Irp WDK 内核，重复使用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 908b910039544ae9de2409af2e89ee9682f316e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377913"
---
# <a name="packet-driven-io-with-reusable-irps"></a>数据包驱动的 I/O 与可重用 IRP





I/O 管理器、 插管理器和使用的电源管理器*I/O 请求数据包*(Irp) 与内核模式驱动程序通信，以允许与彼此进行通信的驱动程序。

I/O 管理器将执行以下步骤：

-   接受通常来源于用户模式应用程序的 I/O 请求。

-   创建 Irp 来表示输入/输出请求。

-   将 Irp 路由到适当的驱动程序。

-   跟踪 Irp 它们完成为止。

-   返回到原始请求方的每个 I/O 操作的状态。

IRP 可能被路由到多个驱动程序。 例如，若要打开磁盘上的文件的请求可能进入第一个文件系统驱动程序，通过中间镜像驱动程序，并最终移到磁盘驱动程序以及可能的即插即用硬件总线驱动程序。 本系列驱动程序被称为*驱动程序堆栈*。

因此，每个 IRP 已*修复部分*，以及一个驱动程序特定*I/O 堆栈位置*每个驱动程序，用于控制设备：

-   中的固定部分 (或*标头*)，I/O 管理器维护原始请求有关的信息，例如调用方的线程 ID 和参数文件是在其的设备对象的地址打开，和等等。 固定的部分还包含*I/O 状态块*，哪些驱动程序中设置请求的 I/O 操作的状态信息。

-   在最高级别的驱动程序的 I/O 堆栈位置、 I/O 管理器、 插管理器中或电源管理器设置特定于驱动程序的参数，如请求的操作和相应的驱动程序使用来确定哪些 it 的上下文的函数代码应执行操作。 反过来，每个驱动程序设置了驱动程序堆栈中的下一步低驱动程序的 I/O 堆栈位置。

每个驱动程序处理 IRP，它可以访问其在 IRP，从而在每个驱动程序的操作阶段重用 IRP 的 I/O 堆栈位置。 此外，更高级别的驱动程序可以创建 （或重用） Irp 发送到更低级别的驱动程序的请求。

Irp 的详细讨论，请参阅[处理 Irp](handling-irps.md)。

 

 




