---
title: 即插即用事件的 NDIS 处理概述
description: 即插即用事件的 NDIS 处理概述
ms.assetid: 3e9ae945-4241-4c66-bdb1-b9e3466167be
keywords:
- 即插即用 WDK NDIS 微型端口，IRP 处理 NIC
- 为 NIC WDK NDIS 处理 IRP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a107c174e55cd523af4dd15a955e8c1b95bdb22d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217026"
---
# <a name="overview-of-ndis-processing-of-plug-and-play-events"></a>即插即用事件的 NDIS 处理概述





网络接口卡的 [功能驱动程序](../kernel/function-drivers.md) (NIC) 实现为 NDIS 和微型端口驱动程序对。 将 NIC 添加到系统时，NDIS 将为 NIC (FDO) 创建功能设备对象。 然后，NDIS 处理所有 Irp，包括传递给此 FDO 的 (PnP) 和电源管理 Irp 即插即用。 NIC 的微型端口驱动程序提供 NIC 的操作接口。\`

以下部分描述了 NDIS 如何代表 NIC 处理 PnP Irp：

[添加 NIC](adding-a-nic.md)

[启动 NIC](starting-a-nic.md)

[停止 NIC](stopping-a-nic.md)

[移除 NIC](removing-a-nic.md)

[处理 NIC 意外删除](processing-the-surprise-removal-of-a-nic.md)

 

