---
title: NDIS 6.20 中对超过 64 个处理器的支持
description: NDIS 6.20 中对超过 64 个处理器的支持
keywords:
- NDIS 6.20 WDK，支持超过64个处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5270f1e9812d9dd44befc81f530e45bddb89187
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825393"
---
# <a name="support-for-more-than-64-processors-in-ndis-620"></a>NDIS 6.20 中对超过 64 个处理器的支持





NDIS 6.20 接口引入了对超过64个处理器的支持。 在 x86 版本的操作系统) 中，以前的 NDIS 版本限制为不超过64处理器 (32。

为了保持与早期版本的向后兼容，NDIS 支持处理器组。 未更新为支持超过64处理器的软件默认情况下为处理器组零。

为了支持64多个处理器，NDIS 6.20 和更高版本提供了这些接口的更新版本：

-   [接收方伸缩 (RSS)](./receive-side-scaling-version-2-rssv2-.md)

-   处理器信息设备驱动程序接口 (参阅 [NDIS 系统信息函数](/windows-hardware/drivers/ddi/_netvista/)) 

-   资源分配 (参阅 [NDIS 内存管理接口](/windows-hardware/drivers/ddi/_netvista/)) 

-   读取和写入锁 (参阅 [NDIS 读取写入锁定引用](/windows-hardware/drivers/ddi/_netvista/)) 

某些 NDIS 设备驱动程序接口元素对于 NDIS 6.20 和更高版本的驱动程序已过时。 有关过时接口的详细信息，请参阅 [NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

 

