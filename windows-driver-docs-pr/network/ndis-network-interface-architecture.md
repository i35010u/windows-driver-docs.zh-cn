---
title: NDIS 网络接口体系结构
description: NDIS 网络接口体系结构
keywords:
- NDIS 网络接口 WDK，体系结构
- 网络接口 WDK、体系结构
ms.date: 02/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: af64374d36b791d19a36ac61f8d03926350c6485
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801573"
---
# <a name="ndis-network-interface-architecture"></a>NDIS 网络接口体系结构

NDIS 提供一组服务以支持网络接口和接口堆栈。 在 WDK 中，这组服务称为 *NDIS 网络接口 (NDISIF)* services。

下图显示了 NDIS 6.0 和更高版本的 NDISIF 体系结构。

![说明 ndis 6.0 网络接口体系结构的关系图](images/ifarch.png)

该体系结构的 NDISIF 组件包括：

- *NDIS IF 服务*  
    一个 NDIS 组件，用于处理接口提供程序和接口的注册，实现 OID 查询并为接口提供程序设置服务，并提供其他 NDISIF 服务。
- *NDIS （如果提供程序接口）*  
    *NDIS IF service* 组件提供的接口，用于启用 ndis 驱动程序以实现接口提供程序。
- *NDIS 代理接口提供程序*  
    一种 NDIS 组件，它代表每个微型端口适配器 (的) 和筛选器驱动程序 (为每个筛选器模块) 实现 NDISIF 提供程序服务。
- *接口提供程序*  
    为 *ndis 代理接口提供程序* 组件无法提供的接口提供 NDISIF 提供程序服务的 NDIS 驱动程序。 例如，MUX 中间驱动程序可以在其虚拟微型端口和基础适配器之间具有内部接口。

NDIS 代理接口提供程序使用标准 NDIS 微型端口驱动程序和 NDIS 筛选器驱动程序接口为微型端口适配器和筛选器模块提供 NDISIF 服务。 因此，无需将微型端口驱动程序和筛选器驱动程序注册为接口提供程序。
