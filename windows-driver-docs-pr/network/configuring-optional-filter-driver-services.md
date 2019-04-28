---
title: 配置可选的筛选器驱动程序服务
description: 配置可选的筛选器驱动程序服务
ms.assetid: 698e1b2a-de1a-435a-bc30-0d27d9e15e19
keywords:
- 筛选器驱动程序 WDK 联网服务
- NDIS 筛选器驱动程序 WDK，服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 843e20db3aa8ee01a3ba6105754273993fcb131c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341413"
---
# <a name="configuring-optional-filter-driver-services"></a>配置可选的筛选器驱动程序服务





NDIS 筛选器驱动程序将调用[ *FilterSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549972)函数以配置可选的筛选器驱动程序服务。 NDIS 调用*FilterSetOptions*筛选器驱动程序的调用的上下文中[ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)函数

*FilterSetOptions*注册的默认入口点的可选*FilterXxx*函数所需的可选服务，并可以分配其他驱动程序资源。 若要注册可选服务，筛选器驱动程序调用[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数，并将传递在特征结构*OptionalHandlers*参数。

当前的 Windows 版本中没有任何可选的筛选器驱动程序服务。

筛选器驱动程序还可以调用**NdisSetOptionalHandlers**设置某些*FilterXxx*函数给定筛选器模块的入口点。 有关详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

如果筛选器驱动程序调用**NdisSetOptionalHandlers**从*FilterRestart*，配置更改仅影响 NDIS 正在重新启动筛选器模块。 其他筛选器模块的配置不受影响。

 

 





