---
title: 同步并行端口的使用
description: 同步并行端口的使用
keywords:
- 并行端口 WDK，同步
- 同步 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25a633b39af05ba32c31979d773431cb51ecc531
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812567"
---
# <a name="synchronizing-the-use-of-a-parallel-port"></a>同步并行端口的使用





客户端必须先通过分配并行端口来对并行端口进行同步，然后再使用它并在使用端口完成后释放端口。

或者，客户端可以选择和取消选择 IEEE 1284.3 设备 (该设备自动分配并释放并行端口) −请参阅 [选择并取消选择附加到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)。

客户端使用以下设备控制请求来分配和释放并行端口：

[**IOCTL \_ 内部 \_ 并行 \_ 端口 \_ 分配**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_port_allocate)

[**IOCTL \_ 内部 \_ 并行 \_ 端口 \_ 免费**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_port_free)

内核模式客户端还可以使用系统提供的 [并行端口回调例程](/windows-hardware/drivers/ddi/index) ，该例程是使用 [**IOCTL \_ 内部 \_ GET \_ 并行 \_ 端口 \_ 信息**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_port_info) 请求获取的。 此请求返回一个 [**并行 \_ 端口 \_ 信息**](/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_port_information) 结构，其中包括指向系统提供的回调的以下指针：

-   **TryAllocatePort** 成员是指向 [*PPARALLEL \_ 尝试 \_ 分配 \_ 例程*](/previous-versions/windows/hardware/drivers/ff544550(v=vs.85))回调的指针，该例程尝试分配并行端口。

-   **QueryNumWaiters** 成员是指向 [*PPARALLEL \_ 查询 \_ 等待进程 \_ 例程*](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_query_waiters_routine)回调的指针，它返回在并行端口的工作队列中排队的端口分配和设备选择请求数。

-   **FreePort** 成员是指向 [*PPARALLEL \_ 免费 \_ 例程*](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_free_routine)回调的指针，它可释放并行端口。

[**IOCTL \_ 内部 \_ 并行 \_ 端口 \_ 分配**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_port_allocate)请求需要客户端的最小处理，因为系统提供的并行端口的函数驱动程序会将客户端的请求排队，前提是已分配了并行端口。 函数驱动程序 \_ 在将端口分配给客户端之后，完成状态为 "成功" 的分配请求。 由于无法接受的超时延迟或一些其他特定于设备的情况，客户端可以随时取消挂起的分配请求。

**注意**  [**PPARALLEL \_ TRY \_ \_**](/previous-versions/windows/hardware/drivers/ff544550(v=vs.85)) (会立即返回 ") 阻止"。 如果客户端仅使用 **PPARALLEL \_ TRY \_ 分配 \_ 例程** 回调来尝试分配其他客户端正在争用的并行端口，则并行端口函数驱动程序可能永远不会将该端口分配给客户端。 若要确保成功，客户端必须使用并行端口分配请求。  (并行端口功能驱动程序队列，随后按接收请求的顺序处理端口分配和设备选择请求。 ) 

 

并行端口功能驱动程序向客户端分配并行端口之后，客户端将具有对端口的独占访问权限。 客户端必须调用 [**PPARALLEL \_ 免费 \_ 例程**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_free_routine) 回调以释放端口。 客户端释放端口后，并行端口函数驱动程序会从端口的工作队列中删除下一个请求， (端口分配或设备 select 请求) （如果有），并完成请求。

客户端应使用 [**PPARALLEL \_ QUERY \_ 等待进程 \_ 例程**](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_query_waiters_routine) 回调来确定是否有其他客户端正在等待并行端口。 需要为长时间分配端口的客户端应定期调用 **PPARALLEL \_ QUERY \_ 等待进程 \_ 例程** 回调来确定其他客户端正在等待获取端口，如果客户端正在等待，请尽快释放端口。

 

