---
title: NDIS 6.1 中的 NetDMA 更新
description: NDIS 6.1 中的 NetDMA 更新
ms.assetid: ec19ac6e-78b3-4da5-baef-e02fc9947c0e
keywords:
- NetDMA WDK 网络，关于 NetDMA 接口
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7d91ee556d825e54bd77e39e2109f721c8835d58
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210667"
---
# <a name="netdma-updates-in-ndis-61"></a>NDIS 6.1 中的 NetDMA 更新

>[!IMPORTANT]
> Windows 8 及更高版本不支持 NetDMA 接口。

NetDMA 接口提供 (DMA) 到支持 NetDMA DMA 引擎 (Nic) 的网络接口卡的直接内存访问。 Windows Server 2008 和 Windows Vista Service Pack 1 (SP1) 操作系统添加 NetDMA 版本1.1 和2.0。 NDIS 6.1 和更高版本的驱动程序可以使用 NetDMA 版本1.0、1.1 和2.0 接口。 这些接口管理与 DMA 引擎的交互，并在运行时管理 DMA 传输。

NetDMA 接口是为 Nic 和其他驱动程序提供的可选服务。

有关 NetDMA 的详细信息，请参阅 [NetDMA 驱动程序](/previous-versions/windows/hardware/network/netdma-drivers)。