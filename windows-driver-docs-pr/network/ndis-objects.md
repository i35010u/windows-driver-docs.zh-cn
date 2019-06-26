---
title: NDIS 对象
description: NDIS 对象
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- 分配了泛型 NDIS 对象
- 泛型 NDIS 对象 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a14525ed88655495c45414659fba4cc0e6393b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354967"
---
# <a name="ndis-objects"></a>NDIS 对象





组件不具有 NDIS 处理使用[ **NdisAllocateGenericObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject)函数来分配泛型 NDIS 对象。 一个组件，必须调用[ **NdisFreeGenericObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreegenericobject)函数来释放与创建一个泛型对象**NdisAllocateGenericObject**。

有关使用泛型对象的信息，请参阅[获取池处理](obtaining-pool-handles.md)。

 

 





