---
title: Plug and Play 事件的 NDIS 处理
description: Plug and Play 事件的 NDIS 处理
ms.assetid: 3e9ae945-4241-4c66-bdb1-b9e3466167be
keywords:
- 即插即用 WDK NDIS 微型端口，nic 处理 IRP
- 为 NIC WDK NDIS 处理 IRP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025b3293bf16b601675fd6fb0c7b37dcc3095f18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547116"
---
# <a name="ndis-processing-of-plug-and-play-events"></a>Plug and Play 事件的 NDIS 处理





[函数的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff546516)为网络接口卡 (NIC) 作为实现的 NDIS 和微型端口驱动程序对。 NDIS NIC 添加到系统中，为 NIC 创建的功能的设备对象 (FDO) NDIS 然后随后处理所有 Irp，包括插即用 (PnP) 和电源管理 Irp，传递给此 FDO。 NIC 的微型端口驱动程序提供用于 NIC 的操作的接口\`

以下部分介绍如何 NDIS 处理 PnP Irp 代表 NIC:

[添加 NIC](adding-a-nic.md)

[启动 NIC](starting-a-nic.md)

[正在停止 NIC](stopping-a-nic.md)

[删除 NIC](removing-a-nic.md)

[处理 NIC 被意外删除](processing-the-surprise-removal-of-a-nic.md)

 

 





