---
title: 添加 NIC
description: 添加 NIC
ms.assetid: 3da89acc-5504-4362-b148-e8228795721f
keywords:
- Nic WDK 网络，并添加
- 网络接口卡 WDK 网络，并添加
- 即插即用 WDK NDIS 微型端口，添加 NIC
- 添加 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d17cb4f22b8329a45bc722a486ef851e246f46e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367781"
---
# <a name="adding-a-nic"></a>添加 NIC





以下说明开头的微型端口驱动程序加载，并介绍如何添加 NIC。 PnP 管理器执行时将 NIC 添加到正在运行的系统的初始处理，请参阅步骤 1-11[添加到运行系统的即插即用设备](https://msdn.microsoft.com/library/windows/hardware/ff540535)。

1.  如果尚未加载的 nic 的微型端口驱动程序，即插即用管理器加载驱动程序，然后调用微型端口驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)函数。 如果尚未加载该驱动程序，处理继续执行步骤 4。

2.  从其**DriverEntry**函数，微型端口驱动程序将注册为微型端口驱动程序并执行其他驱动程序的初始化。 有关注册为微型端口驱动程序的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

3.  NDIS 填充的微型端口驱动程序的驱动程序对象中的以下条目：
    -   入口点*AddDevice*例程。
    -   *DispatchXxx*处理 Irp 的入口点。
    -   入口点*Unload*例程。

4.  PnP 管理器中调用的 NDIS *AddDevice*例程。 NDIS 的*AddDevice*例程为新添加的 NIC 创建功能的设备对象 (FDO)，并将此 FDO 附加到设备堆栈，nic

5.  NDIS 读取信息从注册表获取 NIC 的配置信息 此信息包括绑定信息和 NIC 的硬件属性

6.  PnP 管理器向资源分配到 NIC，如有必要。

 

 





