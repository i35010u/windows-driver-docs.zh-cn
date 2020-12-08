---
title: 添加 NIC
description: 添加 NIC
keywords:
- Nic WDK 网络，添加
- 网络接口卡 WDK 网络，添加
- 即插即用 WDK NDIS 微型端口，添加 NIC
- 添加 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79abac6747426eb7da78a1b97ff0ac5440f75c05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799427"
---
# <a name="adding-a-nic"></a>添加 NIC





以下说明从加载微型端口驱动程序开始，介绍如何添加 NIC。 对于将 NIC 添加到正在运行的系统时，PnP 管理器执行的初始处理，请参阅 [将 PnP 设备添加到正在运行的系统](../kernel/adding-a-pnp-device-to-a-running-system.md)中的步骤1-11。

1.  如果尚未加载 NIC 的微型端口驱动程序，则 PnP 管理器会加载驱动程序，然后调用微型端口驱动程序的 [**DriverEntry**](./initializing-a-miniport-driver.md) 函数。 如果已加载该驱动程序，则继续执行步骤4。

2.  小型端口驱动程序从其 **DriverEntry** 函数注册为微型端口驱动程序并执行其他驱动程序初始化。 有关注册为微型端口驱动程序的详细信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

3.  NDIS 在微型端口驱动程序的驱动程序对象中填充以下项：
    -   *AddDevice* 例程的入口点。
    -   用于处理 Irp 的 *DispatchXxx* 入口点。
    -   *卸载* 例程的入口点。

4.  PnP 管理器调用 NDIS 的 *AddDevice* 例程。 NDIS 的 *AddDevice* 例程为新添加的 NIC 创建一个功能设备对象 (FDO) ，并将此 FDO 附加到 nic 的设备堆栈。

5.  NDIS 读取注册表中的信息以获取 NIC 的配置信息。 此信息包括 NIC 的绑定信息和硬件属性。

6.  如果需要，PnP 管理器会将资源分配给 NIC。

 

