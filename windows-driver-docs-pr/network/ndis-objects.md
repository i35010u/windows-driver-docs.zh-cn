---
title: NDIS 对象
description: NDIS 对象
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- 分配泛型 NDIS 对象
- 一般 NDIS 对象 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b736844f532ea89cf5a67061eede1ec2dfa18b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218003"
---
# <a name="ndis-objects"></a>NDIS 对象





没有 NDIS 句柄的组件使用 [**NdisAllocateGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject) 函数来分配泛型 NDIS 对象。 组件必须调用 [**NdisFreeGenericObject**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject) 函数以释放使用 **NdisAllocateGenericObject**创建的泛型对象。

有关使用泛型对象的信息，请参阅 [获取池句柄](obtaining-pool-handles.md)。

 

