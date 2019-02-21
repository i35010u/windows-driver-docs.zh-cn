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
ms.openlocfilehash: 71d5818dbd50554884bc245bdf8c8ec8dfeb7080
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525605"
---
# <a name="identifying-an-ndis-port"></a>标识 NDIS 端口





NDIS 端口由其端口号标识。 当微型端口驱动程序调用[ **NdisMAllocatePort** ](https://msdn.microsoft.com/library/windows/hardware/ff562779)函数分配一个端口，NDIS 分配并将最小可用的端口号分配给该端口。 当微型端口驱动程序调用[ **NdisMFreePort** ](https://msdn.microsoft.com/library/windows/hardware/ff563588)函数来释放端口、 NDIS 还释放，以便 NDIS 可以重复使用的端口号分配给已释放端口的端口号。

如果驱动程序维护单独的上下文区域的每个端口，该驱动程序必须提供一个高效的算法转换为相应的上下文区域的端口号。

 

 





