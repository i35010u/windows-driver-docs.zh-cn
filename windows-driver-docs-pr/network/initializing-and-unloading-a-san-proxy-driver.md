---
title: 初始化和卸载 SAN 代理驱动程序
description: 初始化和卸载 SAN 代理驱动程序
keywords:
- 代理驱动程序 WDK San，初始化
- SAN 代理驱动程序 WDK，初始化
- 代理驱动程序 WDK San，卸载
- SAN 代理驱动程序 WDK，卸载
- 卸载驱动程序
- 初始化 SAN 代理驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbe39ff1c4e62fad501ee5e641fb86e58a31e7ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816009"
---
# <a name="initializing-and-unloading-a-san-proxy-driver"></a>初始化和卸载 SAN 代理驱动程序





除了为驱动程序对象创建和初始化设备对象之外，还可以注册代理驱动程序的 **DriverEntry** 例程，以便在添加或删除驱动程序控件下的 nic 时获得通知。 有关详细信息，请参阅 [注册 SAN NIC 通知](registering-for-san-nic-notifications.md)。

如果代理驱动程序的 SAN 服务提供程序将 i/o 控制请求发送到代理驱动程序，则 **DriverEntry** 必须指定启用设备控制的 *入口点* 。 例如，提供程序可以请求检索分配给驱动程序的 Nic 的 IP 地址的列表。 此请求的入口点是 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 调度例程，该例程返回分配给驱动程序的 nic 的 IP 地址的列表。 有关详细信息，请参阅为 [SAN 服务提供商实现 IOCTLs](implementing-ioctls-for-a-san-service-provider.md)。

**DriverEntry** 例程必须指定用于卸载代理驱动程序的例程的入口点。 此卸载例程将删除在 **DriverEntry** 中创建的设备。

 

