---
title: 锁定和解锁并行端口
description: 锁定和解锁供并行设备使用的并行端口
keywords:
- 并行设备 WDK，端口锁定/解锁
- 锁定 WDK 并行设备
- 解锁并行端口
- 不间断操作 WDK 并行设备
- 释放并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c542614c59922c542824a0fc7a9a7c914ebfed11
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090982"
---
# <a name="locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device"></a>锁定和解锁供并行设备使用的并行端口





要在并行设备上执行一系列不间断操作，客户端必须分配并行端口，并在端口上选择 IEEE 1284.3 设备。 一系列操作可以包括完成 i/o 请求并执行并行端口总线驱动程序提供的回调例程。 完成一系列操作后，客户端必须取消选择 IEEE 1284.3 设备，然后释放父并行端口。

系统提供的并行端口总线驱动程序支持以下内部设备控制请求来锁定和解锁并行端口：

[**IOCTL \_ 内部 \_ 锁定 \_ 端口**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_lock_port)

[**IOCTL \_ 内部 \_ 锁定 \_ 端口 \_ 未 \_ 选择**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_lock_port_no_select)

[**IOCTL \_ 内部 \_ 解锁 \_ 端口**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_unlock_port)

[**IOCTL \_ 内部 \_ 解锁 \_ 端口 \_ 不能 \_ 取消选择**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_unlock_port_no_deselect)

如果只能使用这些请求提供的功能来操作设备，Microsoft 建议客户端使用锁定端口和解锁端口请求。 否则，客户端可以使用锁定端口 "无选择" 和 "锁定端口" "无取消选择请求"。 这样，客户端就可以更灵活地操作使用选择的设备，并使用不符合 IEEE 1284.3 菊花链规范的 deselection 机制。 客户端可以使用锁定端口 "无选择" 请求来分配端口，然后使用 [设备控制对并行设备](/windows-hardware/drivers/ddi/_parports/) 和 [并行设备回调例程](/windows-hardware/drivers/ddi/_parports/)的请求来操作该设备。

客户端可以向并行设备发送单个 i/o 请求，而无需锁定和解锁并行端口，因为并行端口总线驱动程序在客户端之间管理端口共享。 并行端口总线驱动程序会在处理 i/o 请求之前自动分配并行端口，并且如果有客户端在等待该端口，则在完成 i/o 请求后将立即释放该端口。

如果并行端口总线驱动程序可以在设置的超时期限内将该端口分配给并行设备，则该设备的工作线程将完成该请求。 否则，并行端口总线驱动程序完成挂起的请求，状态为 " \_ 设备 \_ 繁忙"。

 

