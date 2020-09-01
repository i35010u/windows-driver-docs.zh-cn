---
title: 标识 NDIS 端口
description: 标识 NDIS 端口
ms.assetid: 40917e62-5424-4c46-9b5b-a1a15812ef59
keywords:
- 端口 WDK NDIS，identifyng
- NDIS 端口 WDK，identifyng
- identifyng NDIS 端口
- 端口号 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c0a1eafc5e11d7e2b73773cf2f7a9dc738d2e20
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217062"
---
# <a name="identifying-an-ndis-port"></a>标识 NDIS 端口





NDIS 端口由其端口号标识。 当微型端口驱动程序调用 [**NdisMAllocatePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport) 函数来分配端口时，NDIS 会为该端口分配和分配最低可用的端口号。 当微型端口驱动程序调用 [**NdisMFreePort**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) 函数以释放某个端口时，ndis 还会释放分配给已释放端口的端口号，使 ndis 可以重复使用该端口号。

如果驱动程序为每个端口维护单独的上下文区域，则驱动程序必须提供有效的算法将端口号转换为相应的上下文区域。

 

