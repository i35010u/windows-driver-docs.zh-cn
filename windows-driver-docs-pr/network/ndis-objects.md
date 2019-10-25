---
title: NDIS 对象
description: NDIS 对象
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- 分配泛型 NDIS 对象
- 一般 NDIS 对象 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80d506f8a3a2644e3fa014b5777b010379769290
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844360"
---
# <a name="ndis-objects"></a>NDIS 对象





没有 NDIS 句柄的组件使用[**NdisAllocateGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)函数来分配泛型 NDIS 对象。 组件必须调用[**NdisFreeGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject)函数以释放使用**NdisAllocateGenericObject**创建的泛型对象。

有关使用泛型对象的信息，请参阅[获取池句柄](obtaining-pool-handles.md)。

 

 





