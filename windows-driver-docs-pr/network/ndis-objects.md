---
title: NDIS 对象
description: NDIS 对象
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- 分配了泛型 NDIS 对象
- 泛型 NDIS 对象 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67daaa31d7cbe9a46885e5799685da9cb3f0113
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547099"
---
# <a name="ndis-objects"></a>NDIS 对象





组件不具有 NDIS 处理使用[ **NdisAllocateGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561603)函数来分配泛型 NDIS 对象。 一个组件，必须调用[ **NdisFreeGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561850)函数来释放与创建一个泛型对象**NdisAllocateGenericObject**。

有关使用泛型对象的信息，请参阅[获取池处理](obtaining-pool-handles.md)。

 

 





