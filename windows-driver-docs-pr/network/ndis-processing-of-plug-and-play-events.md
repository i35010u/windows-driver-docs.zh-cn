---
title: 即插即用事件的 NDIS 处理概述
description: 即插即用事件的 NDIS 处理概述
keywords:
- 即插即用 WDK NDIS 微型端口，IRP 处理 NIC
- 为 NIC WDK NDIS 处理 IRP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f125ddbdd974e86e25921752ff333006da7fb8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832615"
---
# <a name="overview-of-ndis-processing-of-plug-and-play-events"></a>即插即用事件的 NDIS 处理概述





网络接口卡的 [功能驱动程序](../kernel/function-drivers.md) (NIC) 实现为 NDIS 和微型端口驱动程序对。 将 NIC 添加到系统时，NDIS 将为 NIC (FDO) 创建功能设备对象。 然后，NDIS 处理所有 Irp，包括传递给此 FDO 的 (PnP) 和电源管理 Irp 即插即用。 NIC 的微型端口驱动程序提供 NIC 的操作接口。\`

以下部分描述了 NDIS 如何代表 NIC 处理 PnP Irp：

[添加 NIC](adding-a-nic.md)

[启动 NIC](starting-a-nic.md)

[停止 NIC](stopping-a-nic.md)

[移除 NIC](removing-a-nic.md)

[处理 NIC 意外删除](processing-the-surprise-removal-of-a-nic--windows-vista-.md)

 

