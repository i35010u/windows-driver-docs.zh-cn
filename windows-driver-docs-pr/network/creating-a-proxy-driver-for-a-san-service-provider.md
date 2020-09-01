---
title: 为 SAN 服务提供程序创建代理驱动程序
description: 为 SAN 服务提供程序创建代理驱动程序
ms.assetid: 350c21a3-98e3-48a2-8403-68de97314933
keywords:
- Windows 套接字直接 WDK，代理驱动程序
- 代理驱动程序 WDK San
- SAN 代理驱动程序 WDK
- 代理驱动程序-关于 SAN 代理驱动程序的 WDK San
- SAN 代理驱动程序 WDK，关于 SAN 代理驱动程序
- SAN 服务提供商 WDK，代理驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1655feb54492e801cf9489f6f6984912e065b80b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217682"
---
# <a name="creating-a-proxy-driver-for-a-san-service-provider"></a>为 SAN 服务提供程序创建代理驱动程序





SAN 服务提供程序的代理驱动程序是一个内核模式驱动程序，它执行 Windows 套接字交换机和 SAN 服务提供程序所需的任务。 此类任务包括管理内存和确定网络接口控制器的 IP 地址 (Nic) 在代理驱动程序的控制之下。 代理驱动程序不需要是 Windows 驱动模型 (WDM) 驱动程序。 也就是说，不需要支持即插即用或电源管理。 有关开发内核模式驱动程序的详细信息，请参阅 [内核模式驱动程序组件](../kernel/kernel-mode-driver-components.md)。

不同的供应商可能会使用不同的基础技术来实现 (Nic) 的 SAN 网络接口控制器，因此，Windows Socket Direct 不会在 SAN 服务提供程序与其代理驱动程序之间或在代理驱动程序和 SAN 传输之间指定接口。

SAN NIC 供应商必须实现适用于其基础技术的传输接口。 供应商可以在 san NIC 或 SAN NIC 的内核模式驱动程序中实现此接口。 SAN 服务提供程序将此接口直接映射到用户模式进程的地址空间。 供应商必须确保在此接口上传递的所有缓冲区已锁定并向 SAN NIC 注册。

以下部分介绍如何为 SAN 服务提供程序 DLL 创建代理驱动程序：

[初始化和卸载 SAN 代理驱动程序](initializing-and-unloading-a-san-proxy-driver.md)

[为 SAN 代理驱动程序分配和释放内存](allocating-and-releasing-memory-for-a-san-proxy-driver.md)

[保护和释放虚拟地址所有权](securing-and-releasing-ownership-of-virtual-addresses.md)

[注册 SAN NIC 通知](registering-for-san-nic-notifications.md)

[转换为 SAN 本机地址](translating-to-a-san-native-address.md)

[实现 SAN 服务提供程序的 IOCTL](implementing-ioctls-for-a-san-service-provider.md)

 

