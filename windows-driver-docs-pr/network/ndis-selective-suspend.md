---
title: NDIS 选择性挂起简介
description: NDIS 选择性挂起简介
ms.assetid: B0D44AE3-5197-4264-9838-83FB5EFEB0B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e5d62e9a21e3c2de22121062a3e8e45f0c3f31a
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565661"
---
# <a name="introduction-to-ndis-selective-suspend"></a>NDIS 选择性挂起简介


从 NDIS 6.30 开始, NDIS 选择性挂起接口允许 NDIS 通过将适配器转换为低功耗状态来挂起空闲网络适配器。 这使系统可以减少 CPU 和网络适配器的电源开销。

本部分包括以下主题：

[NDIS 选择性挂起概述](overview-of-ndis-selective-suspend.md)

[报告 NDIS 选择性挂起功能](reporting-ndis-selective-suspend-capabilities.md)

[注册 NDIS 选择性挂起处理程序函数](registering-ndis-selective-suspend-handler-functions.md)

[NDIS 选择性挂起空闲通知](ndis-selective-suspend-idle-notifications.md)

[用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NDIS 选择性挂起实现准则](ndis-selective-suspend-implementation-guidelines.md)

**请注意**  , 虽然 NDIS 选择性挂起接口特别适用于 USB 网络适配器, 但接口与总线无关。 因此, 小型端口驱动程序可以使用其他总线类型上的网络适配器接口来降低 CPU 和电源开销。

 

 

 





