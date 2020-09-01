---
title: 初始化和卸载 SAN 代理驱动程序
description: 初始化和卸载 SAN 代理驱动程序
ms.assetid: 1c602f7d-a1c2-429a-a297-4290a7cbfd9f
keywords:
- 代理驱动程序 WDK San，初始化
- SAN 代理驱动程序 WDK，初始化
- 代理驱动程序 WDK San，卸载
- SAN 代理驱动程序 WDK，卸载
- 卸载驱动程序
- 初始化 SAN 代理驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11dae895ee35b84375de216fb7758ec76aefedc0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206419"
---
# <a name="initializing-and-unloading-a-san-proxy-driver"></a>初始化和卸载 SAN 代理驱动程序





除了为驱动程序对象创建和初始化设备对象之外，还可以注册代理驱动程序的 **DriverEntry** 例程，以便在添加或删除驱动程序控件下的 nic 时获得通知。 有关详细信息，请参阅 [注册 SAN NIC 通知](registering-for-san-nic-notifications.md)。

如果代理驱动程序的 SAN 服务提供程序将 i/o 控制请求发送到代理驱动程序，则 **DriverEntry** 必须指定启用设备控制的 *入口点* 。 例如，提供程序可以请求检索分配给驱动程序的 Nic 的 IP 地址的列表。 此请求的入口点是 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 调度例程，该例程返回分配给驱动程序的 nic 的 IP 地址的列表。 有关详细信息，请参阅为 [SAN 服务提供商实现 IOCTLs](implementing-ioctls-for-a-san-service-provider.md)。

**DriverEntry**例程必须指定用于卸载代理驱动程序的例程的入口点。 此卸载例程将删除在 **DriverEntry**中创建的设备。

 

