---
title: 标识 NDIS 端口
description: 标识 NDIS 端口
keywords:
- 端口 WDK NDIS，identifyng
- NDIS 端口 WDK，identifyng
- identifyng NDIS 端口
- 端口号 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b8633c5aa9da89f41304618b788e191c3636397
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794468"
---
# <a name="identifying-an-ndis-port"></a>标识 NDIS 端口





NDIS 端口由其端口号标识。 当微型端口驱动程序调用 [**NdisMAllocatePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport) 函数来分配端口时，NDIS 会为该端口分配和分配最低可用的端口号。 当微型端口驱动程序调用 [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) 函数以释放某个端口时，ndis 还会释放分配给已释放端口的端口号，使 ndis 可以重复使用该端口号。

如果驱动程序为每个端口维护单独的上下文区域，则驱动程序必须提供有效的算法将端口号转换为相应的上下文区域。

 

