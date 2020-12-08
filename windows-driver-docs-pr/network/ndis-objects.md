---
title: NDIS 对象
description: NDIS 对象
keywords:
- 分配泛型 NDIS 对象
- 一般 NDIS 对象 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 531167b9949e4ffe70cbe7ed2be4e79f0044ef22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783829"
---
# <a name="ndis-objects"></a>NDIS 对象





没有 NDIS 句柄的组件使用 [**NdisAllocateGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject) 函数来分配泛型 NDIS 对象。 组件必须调用 [**NdisFreeGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject) 函数以释放使用 **NdisAllocateGenericObject** 创建的泛型对象。

有关使用泛型对象的信息，请参阅 [获取池句柄](obtaining-pool-handles.md)。

 

