---
title: NDIS 6.1 中的标头数据拆分
description: NDIS 6.1 中的标头数据拆分
keywords:
- 标头-数据拆分 WDK，关于标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e06e47e7b7edbcf980d67e5ad056fb42d2ff22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821359"
---
# <a name="header-data-split-in-ndis-61"></a>NDIS 6.1 中的标头数据拆分





*标头-数据拆分* 服务通过将接收的以太网帧中的标头和数据拆分为单独的缓冲区来改善网络性能。 通过分隔标头和数据，这些服务可将标头一起收集到更小的内存区域中。 因此，在单个内存页中容纳更多的标头，并且系统缓存中容纳更多的标头，因此降低了驱动程序堆栈中内存访问的开销。

标头-数据拆分接口是一种可选服务，为支持标头数据剥离的网络接口卡 (Nic) 提供。

有关标头-数据拆分的详细信息，请参阅 [标头-数据拆分](header-data-split.md)。

 

 





