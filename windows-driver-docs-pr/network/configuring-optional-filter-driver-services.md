---
title: 配置可选的筛选器驱动程序服务
description: 配置可选的筛选器驱动程序服务
ms.assetid: 698e1b2a-de1a-435a-bc30-0d27d9e15e19
keywords:
- 筛选器驱动程序 WDK 网络，服务
- NDIS 筛选器驱动程序 WDK，服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227cc60698e3ee4e5c8a9b4799e9935bc416b6b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838184"
---
# <a name="configuring-optional-filter-driver-services"></a>配置可选的筛选器驱动程序服务





NDIS 调用筛选器驱动程序的[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数来配置可选筛选器驱动程序服务。 NDIS 在筛选器驱动程序调用[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数的上下文中调用*FilterSetOptions*

*FilterSetOptions*为可选服务注册所需的可选*FilterXxx*函数的默认入口点，并可分配其他驱动程序资源。 若要注册可选服务，筛选器驱动程序将调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数，并在*OptionalHandlers*参数处传递特征结构。

当前 Windows 版本中没有可选的筛选器驱动程序服务。

筛选器驱动程序还可以调用**NdisSetOptionalHandlers**来设置给定筛选器模块的某些*FilterXxx*函数入口点。 有关详细信息，请参阅[Data 旁路 Mode](data-bypass-mode.md)。

如果筛选器驱动程序从*FilterRestart*调用**NdisSetOptionalHandlers** ，则配置更改只会影响 NDIS 正在重启的筛选器模块。 其他筛选器模块的配置不受影响。

 

 





