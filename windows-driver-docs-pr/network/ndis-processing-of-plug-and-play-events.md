---
title: 即插即用事件的 NDIS 处理概述
description: 即插即用事件的 NDIS 处理概述
ms.assetid: 3e9ae945-4241-4c66-bdb1-b9e3466167be
keywords:
- 即插即用 WDK NDIS 微型端口, IRP 处理 NIC
- 为 NIC WDK NDIS 处理 IRP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78f9dae42137fb620c9f0d022c758ccacf780461
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565665"
---
# <a name="overview-of-ndis-processing-of-plug-and-play-events"></a>即插即用事件的 NDIS 处理概述





网络接口卡 (NIC) 的[函数驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)实现为 NDIS 和微型端口驱动程序对。 将 NIC 添加到系统时, NDIS 将为 NIC 创建功能设备对象 (FDO)。 然后, NDIS 会处理传递给此 FDO 的所有 Irp, 包括即插即用 (PnP) 和电源管理 Irp。 NIC 的微型端口驱动程序提供 NIC 的操作接口。\`

以下部分描述了 NDIS 如何代表 NIC 处理 PnP Irp:

[添加 NIC](adding-a-nic.md)

[启动 NIC](starting-a-nic.md)

[停止 NIC](stopping-a-nic.md)

[删除 NIC](removing-a-nic.md)

[处理对 NIC 的意外删除](processing-the-surprise-removal-of-a-nic.md)

 

 





