---
title: 锁定和解锁并行端口
description: 锁定和解锁供并行设备使用的并行端口
ms.assetid: dbfa962e-9de8-4a9c-b962-24b53c41f35d
keywords:
- 并行设备 WDK，端口锁定/解锁
- 锁定 WDK 并行设备
- 解锁并行端口
- 不间断操作 WDK 并行设备
- 释放并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a95404992ea7af6cca6ce7ebe96b90d0517060a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845316"
---
# <a name="locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device"></a>锁定和解锁供并行设备使用的并行端口





要在并行设备上执行一系列不间断操作，客户端必须分配并行端口，并在端口上选择 IEEE 1284.3 设备。 一系列操作可以包括完成 i/o 请求并执行并行端口总线驱动程序提供的回调例程。 完成一系列操作后，客户端必须取消选择 IEEE 1284.3 设备，然后释放父并行端口。

系统提供的并行端口总线驱动程序支持以下内部设备控制请求来锁定和解锁并行端口：

[**IOCTL\_内部\_锁定\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_lock_port)

[**IOCTL\_内部\_锁定\_端口\_无\_选择**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_lock_port_no_select)

[**IOCTL\_内部\_解锁\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_unlock_port)

[**IOCTL\_内部\_解锁\_端口\_无\_取消选择**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_unlock_port_no_deselect)

如果只能使用这些请求提供的功能来操作设备，Microsoft 建议客户端使用锁定端口和解锁端口请求。 否则，客户端可以使用锁定端口 "无选择" 和 "锁定端口" "无取消选择请求"。 这样，客户端就可以更灵活地操作使用选择的设备，并使用不符合 IEEE 1284.3 菊花链规范的 deselection 机制。 客户端可以使用锁定端口 "无选择" 请求来分配端口，然后使用[设备控制对并行设备](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的请求来操作该设备。

客户端可以向并行设备发送单个 i/o 请求，而无需锁定和解锁并行端口，因为并行端口总线驱动程序在客户端之间管理端口共享。 并行端口总线驱动程序会在处理 i/o 请求之前自动分配并行端口，并且如果有客户端在等待该端口，则在完成 i/o 请求后将立即释放该端口。

如果并行端口总线驱动程序可以在设置的超时期限内将该端口分配给并行设备，则该设备的工作线程将完成该请求。 否则，并行端口总线驱动程序完成挂起的请求，状态为状态\_设备\_忙。

 

 




