---
title: 在 NDIS 6.1 NetDMA 更新
description: 在 NDIS 6.1 NetDMA 更新
ms.assetid: ec19ac6e-78b3-4da5-baef-e02fc9947c0e
keywords:
- NetDMA WDK 网络、 有关 NetDMA 接口
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6fad15a17d85a824db12bb4817ac89401e1a7e99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369887"
---
# <a name="netdma-updates-in-ndis-61"></a>在 NDIS 6.1 NetDMA 更新

>[!IMPORTANT]
> NetDMA 接口不支持在 Windows 8 和更高版本。

NetDMA 接口提供了支持 NetDMA DMA 引擎的直接内存访问 (DMA) 网络接口卡 (Nic) 的卸载。 Windows Server 2008 和 Windows Vista Service Pack 1 (SP1) 操作系统添加 NetDMA 版本 1.1 和 2.0。 NDIS 6.1 和更高版本的驱动程序可以使用 NetDMA 版本 1.0、 1.1 和 2.0 接口。 这些接口管理与 DMA 引擎之间的交互，并管理在运行时的 DMA 传输。

NetDMA 接口是一项可选服务，提供对 Nic 和其他驱动程序。

NetDMA 有关详细信息，请参阅[NetDMA 驱动程序](netdma-drivers.md)。