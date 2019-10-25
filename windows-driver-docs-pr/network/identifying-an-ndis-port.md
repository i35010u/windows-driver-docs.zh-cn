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
ms.openlocfilehash: 67a63ee26490bd126d2ba1174b19d13aac3573f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823825"
---
# <a name="identifying-an-ndis-port"></a>标识 NDIS 端口





NDIS 端口由其端口号标识。 当微型端口驱动程序调用[**NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocateport)函数来分配端口时，NDIS 会为该端口分配和分配最低可用的端口号。 当微型端口驱动程序调用[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport)函数以释放某个端口时，ndis 还会释放分配给已释放端口的端口号，使 ndis 可以重复使用该端口号。

如果驱动程序为每个端口维护单独的上下文区域，则驱动程序必须提供有效的算法将端口号转换为相应的上下文区域。

 

 





