---
title: 访问设备配置空间
description: 访问设备配置空间
ms.assetid: 082500ae-9df2-4f8b-8be3-ff2b95067a12
keywords:
- I/O WDK 内核，设备配置空间
- 设备配置空间 WDK I/O
- 配置空间 WDK I/O
- 空间 WDK I/O
- 资源信息 WDK I/O
- 驱动程序堆栈 WDK 配置信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f772f9bfa746221fb8295f8384a876a036e0bdd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339140"
---
# <a name="accessing-device-configuration-space"></a>访问设备配置空间





某些总线提供了一种方法访问每个设备连接到总线的特殊配置空间。 本部分介绍如何将驱动程序可以从目标设备的配置空间获取信息提供驱动程序作为功能驱动程序或筛选器驱动程序加载到作为目标设备的驱动程序相同的驱动程序堆栈。

在 Microsoft Windows NT 4.0 中，驱动程序获取的信息从目标设备的配置空间通过扫描总线并调用[ **HalGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff546599)并[ **HalGetBusDataByOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff546606)例程。 在 Windows 2000 和更高版本操作系统中，由其各自的总线驱动程序而不是 HAL 控制硬件总线。 因此，所有的 HAL 例程，用于帮助驱动程序检索总线相关的信息都是在 Windows 2000 中已过时。

设备的配置空间包含的设备和其资源要求的说明。 在 Windows 2000 和更高版本操作系统上，不需要查询来查找资源的设备驱动程序。 该驱动程序获取从 Plug and Play (PnP) 管理器中的资源及其[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 通常情况下，编写良好的驱动程序不需要任何此类信息才能正常工作。 如果由于某种原因，该驱动程序需要使用此信息，该代码示例中[获取设备配置信息在 IRQL = 被动\_级别](obtaining-device-configuration-information-at-irql---passive-level.md)部分演示如何获取的资源。 该驱动程序必须是目标设备的驱动程序堆栈的一部分，因为它需要要发送相应的即插即用请求的目标设备的基础物理设备对象 (PDO)。

 

 




