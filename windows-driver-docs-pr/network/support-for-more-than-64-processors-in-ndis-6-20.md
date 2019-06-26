---
title: NDIS 6.20 中对超过 64 个处理器的支持
description: NDIS 6.20 中对超过 64 个处理器的支持
ms.assetid: 3fb2a09c-e2dd-48b8-a631-3793bd023ef0
keywords:
- NDIS 6.20 WDK，对超过 64 个处理器的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b37c0e070b74cb01ccc1532d4384ac71271cd07d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381170"
---
# <a name="support-for-more-than-64-processors-in-ndis-620"></a>NDIS 6.20 中对超过 64 个处理器的支持





NDIS 6.20 接口引入了多个 64 位处理器的支持。 早期 NDIS 版本仅限于不超过 64 个处理器 (在 x86 的 32 版本的操作系统)。

为了保持向后兼容旧实现 NDIS 支持处理器组。 未更新以支持超过 64 个处理器的软件可以默认为处理器组零。

若要支持超过 64 个处理器，NDIS 6.20 和更高版本提供了这些接口的更新的版本：

-   [接收方缩放 (RSS)](ndis-receive-side-scaling2.md)

-   处理器信息设备驱动程序接口 (请参阅[NDIS 系统信息函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/))

-   资源分配 (请参阅[NDIS 内存管理界面](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/))

-   读取和写锁 (请参阅[NDIS 读写锁引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/))

NDIS 设备驱动程序界面元素的某些已过时的 NDIS 6.20 和更高版本的驱动程序。 有关已过时的接口的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

 

 





