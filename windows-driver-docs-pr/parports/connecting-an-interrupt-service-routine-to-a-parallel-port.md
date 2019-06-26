---
title: 将中断服务例程连接到并行端口
description: 将中断服务例程连接到并行端口
ms.assetid: 62d3a388-6de6-4019-ab95-56b5e96d0891
keywords:
- 并行端口 WDK，中断服务例程
- 中断服务例程 WDK 的并行端口
- 延迟的端口检查例程 WDK 的并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23ea5df80cbd7487233397e94ea52b2b04a9e12a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385989"
---
# <a name="connecting-an-interrupt-service-routine-to-a-parallel-port"></a>将中断服务例程连接到并行端口





内核模式下客户端可以使用[ **IOCTL\_内部\_并行\_CONNECT\_中断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parallel_connect_interrupt)请求连接中断服务例程和一个*延迟端口检查例程*并行端口功能驱动程序的操作。

**请注意**   Microsoft 不建议使用客户端提供中断例程。 中断的使用可能会导致系统不稳定。 默认情况下，IOCTL\_内部\_并行\_CONNECT\_中断请求将被禁用。

 

为了便于移植和并行设备的驱动程序开发，并行端口的系统提供的函数驱动程序支持内核模式下客户端可用来启用和禁用连接中断请求的注册表标志。 连接中断请求启用由注册表项值**EnableConnectInterruptIoctl**并行端口插注册表项下。 将项值具有类型 REG\_DWORD 和默认值为 0x0 （禁用）。 一个值不等于 0x0，可实现连接中断请求。

连接中断请求返回[**并行\_中断\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ns-parallel-_parallel_interrupt_information)结构，其中包含指向并行端口的中断对象的指针和以下系统提供的回调例程的指针：

-   **TryAllocatePortAtInterruptLevel**成员是指向的非阻止性[ *PPARALLEL\_尝试\_分配\_例程 (ISR)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_try_allocate_routine)回调，它在内核模式驱动程序可用于在 ISR 中分配的并行端口。

-   **FreePortFromInterruptLevel**成员是指向的非阻止性[ *PPARALLEL\_免费\_例程 (ISR)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/nc-parallel-pparallel_free_routine)回调，内核模式驱动程序可以使用 ISR，若要释放并行端口。

中断服务例程调用在 IRQL = DIRQL 后并行端口上的硬件中断。 如果驱动程序连接中断服务例程，并具有**Unload**例程，驱动程序必须发送[ **IOCTL\_内部\_并行\_断开连接\_中断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_parallel_disconnect_interrupt)请求在其**卸载**例程。

延迟的端口检查例程称为并行端口将被释放后，没有任何挂起的请求无法分配端口，或选择 IEEE 1284.3 设备时。 驱动程序可以使用延迟的端口检查例程来启用的中断。

如果客户端的中断服务例程称为客户端没有分配的端口时，客户端可以尝试快速分配端口通过调用 PPARALLEL\_尝试\_分配\_例程 (ISR) 回调。 客户端还可以使用 PPARALLEL\_免费\_例程 (ISR) 回调以释放该端口。

由于并行端口共享的驱动程序中，并行端口功能驱动程序维护的中断服务例程和延迟的端口检查例程连接到并行端口的列表。 并行端口函数驱动程序调用所有连接中断例程和延迟的端口检查已连接的顺序中的例程。

 

 




