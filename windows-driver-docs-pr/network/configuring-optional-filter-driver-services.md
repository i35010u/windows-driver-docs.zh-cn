---
title: 配置可选的筛选器驱动程序服务
description: 配置可选的筛选器驱动程序服务
ms.assetid: 698e1b2a-de1a-435a-bc30-0d27d9e15e19
keywords:
- 筛选器驱动程序 WDK 网络，服务
- NDIS 筛选器驱动程序 WDK，服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8680d5bace33d1244c80847c70af2102dddc2bb6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212945"
---
# <a name="configuring-optional-filter-driver-services"></a>配置可选的筛选器驱动程序服务





NDIS 调用筛选器驱动程序的 [*FilterSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数来配置可选筛选器驱动程序服务。 NDIS 在筛选器驱动程序调用[**NdisFRegisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数的上下文中调用*FilterSetOptions*

*FilterSetOptions* 为可选服务注册所需的可选 *FilterXxx* 函数的默认入口点，并可分配其他驱动程序资源。 若要注册可选服务，筛选器驱动程序将调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) 函数，并在 *OptionalHandlers* 参数处传递特征结构。

当前 Windows 版本中没有可选的筛选器驱动程序服务。

筛选器驱动程序还可以调用 **NdisSetOptionalHandlers** 来设置给定筛选器模块的某些 *FilterXxx* 函数入口点。 有关详细信息，请参阅 [Data 旁路 Mode](data-bypass-mode.md)。

如果筛选器驱动程序从*FilterRestart*调用**NdisSetOptionalHandlers** ，则配置更改只会影响 NDIS 正在重启的筛选器模块。 其他筛选器模块的配置不受影响。

 

