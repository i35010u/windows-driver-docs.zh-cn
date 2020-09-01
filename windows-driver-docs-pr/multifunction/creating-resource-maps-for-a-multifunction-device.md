---
title: 为多功能设备创建资源映射
description: 为多功能设备创建资源映射
ms.assetid: 332eef11-4056-4fe0-87ed-4305c091bab1
keywords:
- 多功能设备 WDK，资源映射
- 资源映射 WDK 多功能设备
- 子函数资源映射 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c1f3d83df878387a598aece16a7f5f0de82a3ec
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185903"
---
# <a name="creating-resource-maps-for-a-multifunction-device"></a>为多功能设备创建资源映射





*资源映射*标识子函数使用的多功能设备的资源。 使用 [**INF AddReg 指令**](../install/inf-addreg-directive.md)指定资源映射。 如果多功能设备需要资源映射，则设备的 INF 通常包含设备的每个功能的资源映射。

资源映射分为两种类型： *标准* 资源映射和 *不同* 资源映射。 本部分介绍如何构造资源映射，并包括以下主题：

[创建标准资源映射](creating-standard-resource-maps.md)

[创建可变资源映射](creating-varying-resource-maps.md)

某些多功能设备只能使用标准资源映射进行描述。 其他一些要求不同的资源映射，或者标准和不同映射的组合。 其他人根本不需要资源映射。 请参阅 [支持多功能 PC 卡设备](supporting-multifunction-pc-card-devices.md) ，以确定哪些多功能设备需要资源映射。

 

