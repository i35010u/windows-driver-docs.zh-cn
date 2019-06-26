---
title: 即插即用事件的 NDIS 处理
description: 即插即用事件的 NDIS 处理
ms.assetid: 3e9ae945-4241-4c66-bdb1-b9e3466167be
keywords:
- 即插即用 WDK NDIS 微型端口，nic 处理 IRP
- 为 NIC WDK NDIS 处理 IRP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28748e9617675672485ddb54f817b5790f7cfe31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370592"
---
# <a name="ndis-processing-of-plug-and-play-events"></a>即插即用事件的 NDIS 处理





[函数的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)为网络接口卡 (NIC) 作为实现的 NDIS 和微型端口驱动程序对。 NDIS NIC 添加到系统中，为 NIC 创建的功能的设备对象 (FDO) NDIS 然后随后处理所有 Irp，包括插即用 (PnP) 和电源管理 Irp，传递给此 FDO。 NIC 的微型端口驱动程序提供用于 NIC 的操作的接口\`

以下部分介绍如何 NDIS 处理 PnP Irp 代表 NIC:

[添加 NIC](adding-a-nic.md)

[启动 NIC](starting-a-nic.md)

[正在停止 NIC](stopping-a-nic.md)

[删除 NIC](removing-a-nic.md)

[处理 NIC 被意外删除](processing-the-surprise-removal-of-a-nic.md)

 

 





