---
title: 同步并行端口的使用
description: 同步并行端口的使用
ms.assetid: ea3a1998-9e31-4047-9193-6b402db222c9
keywords:
- 并行端口 WDK，同步
- 同步 WDK 的并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8c80c9b261b793a240d40d82ccfacd18bb2698
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371073"
---
# <a name="synchronizing-the-use-of-a-parallel-port"></a>同步并行端口的使用





客户端必须通过将分配给前使用它和它们完成后释放该端口的并行端口同步其使用并行端口使用它。

客户端可以选择或取消选择 （这会自动分配和释放并行端口） 的 IEEE 1284.3 设备或者，请参阅 −[选择和取消选择 IEEE 1284 设备附加到并行端口](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)。

客户端使用以下设备控制请求分配和释放并行端口：

[**IOCTL\_INTERNAL\_PARALLEL\_PORT\_ALLOCATE**](https://msdn.microsoft.com/library/windows/hardware/ff544023)

[**IOCTL\_INTERNAL\_PARALLEL\_PORT\_FREE**](https://msdn.microsoft.com/library/windows/hardware/ff544026)

内核模式下客户端还可以使用系统提供[并行端口回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544307)通过使用获得[ **IOCTL\_内部\_获取\_并行\_端口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544002)请求。 此请求将返回[**并行\_端口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544322)结构，它包括以下指向系统提供的回调：

-   **TryAllocatePort**成员是指向[ *PPARALLEL\_尝试\_分配\_例程*](https://msdn.microsoft.com/library/windows/hardware/ff544550)回调，即尝试分配并行端口的非阻止性例程。

-   **QueryNumWaiters**成员是指向[ *PPARALLEL\_查询\_等待者\_例程*](https://msdn.microsoft.com/library/windows/hardware/ff544532)回调，它返回分配端口号和设备选择并行端口的工作队列排队的请求。

-   **FreePort**成员是指向[ *PPARALLEL\_免费\_例程*](https://msdn.microsoft.com/library/windows/hardware/ff544509)回调，从而使并行端口。

[ **IOCTL\_内部\_并行\_端口\_分配**](https://msdn.microsoft.com/library/windows/hardware/ff544023)请求要求最少处理由客户端，因为系统提供如果已分配的并行端口，功能驱动程序的并行端口队列客户端的请求。 功能驱动程序完成状态的状态的分配请求\_成功后会将该端口分配给客户端。 由于不能接受超时延迟或某些其他特定于设备的条件，客户端可以在任何时候取消挂起的分配请求。

**请注意**   [ **PPARALLEL\_尝试\_分配\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff544550)回调会立即返回 (为非阻止性)。 如果客户端仅使用**PPARALLEL\_尝试\_分配\_例程**回调以尝试分配并行端口的其他客户端在争用，并行端口功能驱动程序可能永远不会将该端口分配给客户端。 若要确保成功，客户端必须使用并行端口分配请求。 （并行端口函数驱动程序队列和随后的进程，端口分配和设备在其中接收请求的顺序选择请求）。

 

并行端口功能驱动程序会将并行端口分配到客户端后，客户端具有独占访问权限的端口。 客户端必须调用[ **PPARALLEL\_免费\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff544509)回调以释放该端口。 客户端释放该端口后，并行端口功能驱动程序中删除下一个请求 （端口分配或设备选择请求），如果任何端口的工作进行排队并在完成请求。

客户端应使用[ **PPARALLEL\_查询\_等待者\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff544532)回调，以确定是否存在等待并行端口的其他客户端。 需要分配一个端口，对于长的时间的时间应定期调用的客户端**PPARALLEL\_查询\_等待者\_例程**回调，以确定其他客户端处于等待状态为获取该端口，并且如果在等待客户端，请尽快释放该端口。

 

 




