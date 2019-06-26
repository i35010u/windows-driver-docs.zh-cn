---
title: 为 SAN 服务提供程序创建代理驱动程序
description: 为 SAN 服务提供程序创建代理驱动程序
ms.assetid: 350c21a3-98e3-48a2-8403-68de97314933
keywords:
- Windows 套接字直接 WDK，代理驱动程序
- 代理驱动程序 WDK San
- SAN 代理驱动程序 WDK
- 代理驱动程序 WDK San、 SAN 代理驱动程序
- SAN 代理驱动程序 WDK，有关 SAN 代理驱动程序
- SAN 服务提供商 WDK，代理驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54a6c6ec198c82a1232caf38b2ec81949eb3061e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374924"
---
# <a name="creating-a-proxy-driver-for-a-san-service-provider"></a>为 SAN 服务提供程序创建代理驱动程序





SAN 服务提供程序的代理驱动程序是一个内核模式驱动程序执行任务所需的 Windows 套接字开关和 SAN 服务提供商。 此类任务包括管理内存和确定代理驱动程序的控制下的网络接口控制器 (Nic) 的 IP 地址。 代理驱动程序不需要是 Windows 驱动程序模型 (WDM) 驱动程序。 也就是说，不需要支持插或电源管理。 有关开发的内核模式驱动程序的详细信息，请参阅[内核模式驱动程序组件](https://docs.microsoft.com/windows-hardware/drivers/kernel/kernel-mode-driver-components)。

不同供应商可能使用不同的基础技术来实现其 SAN 网络接口控制器 (Nic)，因此 Windows 套接字直接未指定代理服务器之间或 SAN 服务提供程序和其代理驱动程序之间的接口驱动程序和 SAN 传输。

SAN NIC 供应商必须实现适用于其基础技术传输接口。 供应商可以在 SAN NIC，和 / 或 SAN NIC，到内核模式驱动程序中实现此接口。 SAN 服务提供程序将此接口映射直接在用户模式进程的地址空间。 供应商必须确保通过此接口传递的所有缓冲区都锁住并注册到 SAN nic。

以下部分介绍如何为 SAN 服务提供程序 DLL 创建一个代理驱动程序：

[初始化和卸载 SAN 代理驱动程序](initializing-and-unloading-a-san-proxy-driver.md)

[为分配和释放内存的 SAN 代理驱动程序](allocating-and-releasing-memory-for-a-san-proxy-driver.md)

[保护和释放虚拟地址的所有权](securing-and-releasing-ownership-of-virtual-addresses.md)

[注册 SAN NIC 通知](registering-for-san-nic-notifications.md)

[转换到 SAN 本机地址](translating-to-a-san-native-address.md)

[实现 Ioctl SAN 服务提供程序](implementing-ioctls-for-a-san-service-provider.md)

 

 





