---
title: 初始化和卸载 SAN 代理驱动程序
description: 初始化和卸载 SAN 代理驱动程序
ms.assetid: 1c602f7d-a1c2-429a-a297-4290a7cbfd9f
keywords:
- 代理驱动程序 WDK San，初始化
- SAN 代理驱动程序 WDK，初始化
- 代理驱动程序 WDK San、 卸载
- SAN 代理驱动程序 WDK，卸载
- 正在卸载驱动程序
- 初始化 SAN 代理驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5774e5e9aef58fdc2589e9d91621d967f373d5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324940"
---
# <a name="initializing-and-unloading-a-san-proxy-driver"></a>初始化和卸载 SAN 代理驱动程序





除了创建和初始化设备对象驱动程序对象的代理驱动程序**DriverEntry**例程可以注册驱动程序的控制下的 Nic 可以添加或删除时收到通知。 有关详细信息，请参阅[注册 SAN NIC 通知](registering-for-san-nic-notifications.md)。

如果代理驱动程序的 SAN 服务提供商发送 I/O 控制请求向代理驱动程序，然后**DriverEntry**必须指定*入口点*，使设备控制。 访问接口可能会将请求，例如，若要检索的 IP 地址分配给 Nic 驱动程序的列表。 此请求的入口点是[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)调度例程，以返回分配给驱动程序的 Nic 的 IP 地址的列表。 有关详细信息，请参阅[SAN 服务提供程序实现 Ioctl](implementing-ioctls-for-a-san-service-provider.md)。

**DriverEntry**例程必须指定卸载代理驱动程序的例程的入口点。 此卸载例程中删除设备中创建**DriverEntry**。

 

 





