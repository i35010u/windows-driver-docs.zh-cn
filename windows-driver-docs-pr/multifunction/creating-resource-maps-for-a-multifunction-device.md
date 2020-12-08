---
title: 为多功能设备创建资源映射
description: 为多功能设备创建资源映射
keywords:
- 多功能设备 WDK，资源映射
- 资源映射 WDK 多功能设备
- 子函数资源映射 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ffa9c917a912214fc7c72bdd6aff6dbe2d6dfb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820613"
---
# <a name="creating-resource-maps-for-a-multifunction-device"></a>为多功能设备创建资源映射





*资源映射* 标识子函数使用的多功能设备的资源。 使用 [**INF AddReg 指令**](../install/inf-addreg-directive.md)指定资源映射。 如果多功能设备需要资源映射，则设备的 INF 通常包含设备的每个功能的资源映射。

资源映射分为两种类型： *标准* 资源映射和 *不同* 资源映射。 本部分介绍如何构造资源映射，并包括以下主题：

[创建标准资源映射](creating-standard-resource-maps.md)

[创建可变资源映射](creating-varying-resource-maps.md)

某些多功能设备只能使用标准资源映射进行描述。 其他一些要求不同的资源映射，或者标准和不同映射的组合。 其他人根本不需要资源映射。 请参阅 [支持多功能 PC 卡设备](supporting-multifunction-pc-card-devices.md) ，以确定哪些多功能设备需要资源映射。

 

