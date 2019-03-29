---
title: NDIS 网络接口体系结构
description: NDIS 网络接口体系结构
ms.assetid: ce51008e-678c-421c-b796-36baab3df6b3
keywords:
- NDIS 网络接口 WDK，体系结构
- 网络接口 WDK，体系结构
ms.date: 02/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4a72908c43bf8ffd7cdfc6ec0c3e1ece1ca83da1
ms.sourcegitcommit: b13e6d44c71197971697f710c0ecb23db13fea91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203930"
---
# <a name="ndis-network-interface-architecture"></a>NDIS 网络接口体系结构

NDIS 提供了一组服务，以支持网络接口和接口堆栈。 在 WDK 中，这组服务被称为*NDIS 网络接口 (NDISIF)* 服务。

下图显示了 NDISIF 体系结构为 NDIS 6.0 及更高版本。

![说明 ndis 6.0 网络接口体系结构的关系图](images/ifarch.png)

体系结构的 NDISIF 组件包括：

- *NDIS IF Services*  
    处理的接口提供程序和接口，注册的 NDIS 组件实现 OID 查询，并设置为接口提供程序服务，并提供了其他 NDISIF 服务。
- *NDIS 如果提供程序接口*  
    一个接口， *NDIS 如果服务*组件提供以启用 NDIS 驱动程序来实现接口提供程序。
- *NDIS 代理接口提供程序*  
    一种 NDIS 组件实现 NDISIF 提供程序服务代表 NDIS 微型端口驱动程序 （适用于每个微型端口适配器） 和 （适用于每个筛选器模块） 的筛选器驱动程序。
- *接口提供程序*  
    提供有关 NDISIF 提供程序服务的 NDIS 驱动程序的接口*NDIS 代理接口提供程序*组件不能提供。 例如，MUX 中间驱动程序可以有其虚拟微型端口和基础适配器之间的内部接口。

NDIS 代理接口提供程序使用的标准 NDIS 微型端口驱动程序和 NDIS 筛选器驱动程序接口提供用于微型端口适配器 NDISIF 服务和筛选器模块。 因此，微型端口驱动程序和筛选器驱动程序不需要注册为接口提供程序。