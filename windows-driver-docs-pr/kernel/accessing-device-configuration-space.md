---
title: 访问设备配置空间
description: 访问设备配置空间
ms.assetid: 082500ae-9df2-4f8b-8be3-ff2b95067a12
keywords:
- I/o WDK 内核，设备配置空间
- 设备配置空间 WDK i/o
- 配置空间 WDK i/o
- 太空 WDK i/o
- 资源信息 WDK i/o
- 驱动程序堆栈 WDK 配置信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fea847a5e770b9958ef4813929eeb016949c8f92
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189099"
---
# <a name="accessing-device-configuration-space"></a>访问设备配置空间





某些总线为连接到总线的每个设备提供一种访问特殊配置空间的方法。 本部分介绍了当驱动程序作为功能驱动程序或筛选器驱动程序加载到与目标设备的驱动程序相同的驱动程序堆栈中时，驱动程序如何从目标设备的配置空间获取信息。

在 Microsoft Windows NT 4.0 中，驱动程序通过扫描总线并调用 [**HalGetBusData**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 和 [**HalGetBusDataByOffset**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 例程从目标设备的配置空间中获取信息。 在 Windows 2000 和更高版本的操作系统中，硬件总线由其各自的总线驱动程序而不是 HAL 控制。 因此，用于帮助驱动程序检索与总线相关的信息的所有 HAL 例程在 Windows 2000 中已过时。

设备的配置空间包含设备及其资源要求的描述。 在 Windows 2000 和更高版本的操作系统上，驱动程序不需要查询设备来查找资源。 驱动程序将从其 [**IRP \_ MN \_ START \_ DEVICE**](./irp-mn-start-device.md) 请求中的即插即用 (PnP) 管理器获取资源。 通常，编写完善的驱动程序不需要任何此信息即可正常运行。 如果由于某种原因，驱动程序需要此信息，则在 "以 [IRQL = 被动 \_ 级别获取设备配置信息](obtaining-device-configuration-information-at-irql---passive-level.md) " 部分中的代码示例将演示如何获取资源。 驱动程序必须是目标设备的驱动程序堆栈的一部分，因为它需要目标设备 (PDO) 的基础物理设备对象来发送适当的 PnP 请求。

 

