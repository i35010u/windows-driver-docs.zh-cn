---
title: 将中断服务例程连接到并行端口
description: 将中断服务例程连接到并行端口
keywords:
- 并行端口 WDK，中断服务例程
- 中断服务例程 WDK 并行端口
- 延迟的端口检查例程 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c765c8f60c4f9bbe12de04449a80df90321b2f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812645"
---
# <a name="connecting-an-interrupt-service-routine-to-a-parallel-port"></a>将中断服务例程连接到并行端口





内核模式客户端可以使用 [**IOCTL \_ 内部 \_ 并行 \_ 连接 \_ 中断**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_connect_interrupt) 请求将中断服务例程和 *延迟端口检查例程* 连接到并行端口功能驱动程序的操作。

**注意**   Microsoft 不建议使用客户端提供的中断例程。 中断的使用可能会导致系统不稳定。 默认情况下，IOCTL \_ 内部 \_ 并行 \_ 连接 \_ 中断请求处于禁用状态。

 

为了便于移植和开发并行设备的驱动程序，系统提供的并行端口函数驱动程序支持一个注册表标志，内核模式客户端可以使用该标志来启用和禁用连接中断请求。 连接中断请求由 **EnableConnectInterruptIoctl** 的注册表项值在并行端口的即插即用注册表项中启用。 条目值的类型为 REG \_ DWORD，默认值为 0x0 (禁用) 。 不等于0x0 的值将启用连接中断请求。

连接中断请求将返回 [**并行 \_ 中断 \_ 信息**](/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_interrupt_information) 结构，该结构包含指向并行端口中断对象的指针和指向系统提供的回调例程的以下指针：

-   **TryAllocatePortAtInterruptLevel** 成员是指向非阻止 PPARALLEL 的指针 [*。 \_ 尝试 \_ 分配 \_ 例程 () ISR*](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_try_allocate_routine) ，这是一个内核模式驱动程序可在 isr 中用来分配并行端口的回调。

-   **FreePortFromInterruptLevel** 成员是指向非阻止 [*PPARALLEL \_ 免费 \_ 例程 () isr*](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_free_routine)的指针，它可以在 isr 中使用内核模式驱动程序来释放并行端口。

当并行端口上的硬件中断后，中断服务例程在 IRQL = DIRQL 上调用。 如果驱动程序连接中断服务例程并具有 **卸载** 例程，则驱动程序必须在其 **卸载** 例程中发送 [**IOCTL \_ 内部 \_ 并行 \_ 断开连接 \_ 中断**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_disconnect_interrupt)请求。

当并行端口被释放并且没有挂起的请求来分配端口或选择 IEEE 1284.3 设备时，将调用延迟的端口检查例程。 驱动程序可以使用延迟的端口检查例程来启用中断。

如果客户端的中断服务例程是在客户端未分配端口时调用的，则客户端可以通过调用 PPARALLEL \_ TRY \_ ALLOCATE \_ (ISR) 回调来尝试快速分配端口。 客户端还可以使用 PPARALLEL \_ 免费 \_ 例程 (ISR) 回调来释放端口。

由于并行端口由驱动程序共享，因此并行端口功能驱动程序会保留中断服务例程列表和连接到并行端口的延迟端口检查例程的列表。 并行端口函数驱动程序按连接的顺序调用所有连接的中断例程和延迟的端口检查例程。

 

