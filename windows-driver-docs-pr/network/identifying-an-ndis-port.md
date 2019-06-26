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
ms.openlocfilehash: e300f9b14e3bbe3eae24ec3c47ef3b86f2f7ca38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384552"
---
# <a name="identifying-an-ndis-port"></a>标识 NDIS 端口





NDIS 端口由其端口号标识。 当微型端口驱动程序调用[ **NdisMAllocatePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocateport)函数分配一个端口，NDIS 分配并将最小可用的端口号分配给该端口。 当微型端口驱动程序调用[ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)函数来释放端口、 NDIS 还释放，以便 NDIS 可以重复使用的端口号分配给已释放端口的端口号。

如果驱动程序维护单独的上下文区域的每个端口，该驱动程序必须提供一个高效的算法转换为相应的上下文区域的端口号。

 

 





