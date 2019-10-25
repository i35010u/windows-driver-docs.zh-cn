---
title: NDIS 6.20 中对超过 64 个处理器的支持
description: NDIS 6.20 中对超过 64 个处理器的支持
ms.assetid: 3fb2a09c-e2dd-48b8-a631-3793bd023ef0
keywords:
- NDIS 6.20 WDK，支持超过64个处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2712415bf1f98b72c97dd3489f05a6ee6280338
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841803"
---
# <a name="support-for-more-than-64-processors-in-ndis-620"></a>NDIS 6.20 中对超过 64 个处理器的支持





NDIS 6.20 接口引入了对超过64个处理器的支持。 以前的 NDIS 版本限制为在 x86 版本的操作系统中不超过64个处理器（32）。

为了保持与早期版本的向后兼容，NDIS 支持处理器组。 未更新为支持超过64处理器的软件默认情况下为处理器组零。

为了支持64多个处理器，NDIS 6.20 和更高版本提供了这些接口的更新版本：

-   [接收方缩放（RSS）](ndis-receive-side-scaling2.md)

-   处理器信息设备驱动程序接口（请参阅[NDIS 系统信息函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)）

-   资源分配（请参阅[NDIS 内存管理接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)）

-   读取和写入锁定（请参阅[NDIS 读取写入锁定引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)）

某些 NDIS 设备驱动程序接口元素对于 NDIS 6.20 和更高版本的驱动程序已过时。 有关过时接口的详细信息，请参阅[NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

 

 





