---
title: NDIS 6.1 中的标头数据拆分
description: NDIS 6.1 中的标头数据拆分
ms.assetid: f4380956-b18b-46f4-9c2e-d8124cbf5c3f
keywords:
- 标头数据拆分 WDK，有关标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3fcabef751fc85b7ed56c92bfc0fe79fcd9cede
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542844"
---
# <a name="header-data-split-in-ndis-61"></a>NDIS 6.1 中的标头数据拆分





*标头数据拆分*服务通过将标头和接收到的以太网帧中的数据拆分为单独的缓冲区来提高网络性能。 通过将标头和数据，这些服务，要收集在一起分成若干个较小的内存区域的标头。 因此，多个标头放入单个内存页和多个标头放入系统缓存，因此在访问内存的开销减少驱动程序堆栈。

标头数据拆分接口是一项可选服务提供的标头的数据-拆分的网络接口卡 (Nic)。

标头数据拆分的详细信息，请参阅[标头数据拆分](header-data-split.md)。

 

 





