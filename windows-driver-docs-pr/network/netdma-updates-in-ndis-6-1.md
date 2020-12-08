---
title: NDIS 6.1 中的 NetDMA 更新
description: NDIS 6.1 中的 NetDMA 更新
keywords:
- NetDMA WDK 网络，关于 NetDMA 接口
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: e3c29e1012602e8fcd36496f49fe889b736a333c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809993"
---
# <a name="netdma-updates-in-ndis-61"></a>NDIS 6.1 中的 NetDMA 更新

>[!IMPORTANT]
> Windows 8 及更高版本不支持 NetDMA 接口。

NetDMA 接口提供 (DMA) 到支持 NetDMA DMA 引擎 (Nic) 的网络接口卡的直接内存访问。 Windows Server 2008 和 Windows Vista Service Pack 1 (SP1) 操作系统添加 NetDMA 版本1.1 和2.0。 NDIS 6.1 和更高版本的驱动程序可以使用 NetDMA 版本1.0、1.1 和2.0 接口。 这些接口管理与 DMA 引擎的交互，并在运行时管理 DMA 传输。

NetDMA 接口是为 Nic 和其他驱动程序提供的可选服务。

有关 NetDMA 的详细信息，请参阅 [NetDMA 驱动程序](/previous-versions/windows/hardware/network/netdma-drivers)。
