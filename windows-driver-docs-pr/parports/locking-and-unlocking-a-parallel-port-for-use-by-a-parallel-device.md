---
title: 锁定和解锁并行端口
description: 锁定和解锁供并行设备使用的并行端口
ms.assetid: dbfa962e-9de8-4a9c-b962-24b53c41f35d
keywords:
- 并行设备 WDK，端口锁定/解锁
- 锁定 WDK 并行设备
- 解锁的并行端口
- 实现不间断的操作 WDK 并行设备
- 释放的并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ba5df9afa0a54eb78d875ec4b8ce81218dcfc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358516"
---
# <a name="locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device"></a>锁定和解锁供并行设备使用的并行端口





若要执行不间断的并行设备上的操作序列，客户端必须分配并行端口并选择的端口上的 IEEE 1284.3 设备。 完成 I/O 请求并执行并行端口总线驱动程序提供的回调例程可以包含一系列操作。 完成后一系列操作，客户端必须取消选择 IEEE 1284.3 设备，然后释放父并行端口。

并行端口的系统提供的总线驱动程序支持以下内置设备控制请求以锁定和解锁的并行端口：

[**IOCTL\_INTERNAL\_LOCK\_PORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_lock_port)

[**IOCTL\_INTERNAL\_LOCK\_PORT\_NO\_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_lock_port_no_select)

[**IOCTL\_INTERNAL\_UNLOCK\_PORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_unlock_port)

[**IOCTL\_INTERNAL\_UNLOCK\_PORT\_NO\_DESELECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_unlock_port_no_deselect)

Microsoft 建议客户端使用的锁端口并解锁端口请求，如果设备可以通过仅使用这些请求提供的功能操作。 否则为客户端可以使用锁端口没有 select 和锁定端口没有取消选择的请求。 这提供了客户端更大的灵活性以运行使用不符合 IEEE 1284.3 菊花链规范的选择和取消选择机制的设备。 客户端可以使用任何选择的请求分配端口，锁定端口，然后通过运行设备[并行的设备的设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)并[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

客户端可以发送到并行设备而无需锁定和解锁的并行端口，因为并行端口总线驱动程序管理端口在客户端之间共享单个 I/O 请求。 并行端口总线驱动程序会自动分配的并行端口立即处理 I/O 请求和前，如果客户端端口，正在等待完成 I/O 请求之后立即释放该端口。

如果并行端口总线驱动程序可以将该端口分配期间，到并行设备设置超时内设备的工作线程完成请求。 否则，并行端口总线驱动程序完成状态的状态挂起的请求\_设备\_忙。

 

 




