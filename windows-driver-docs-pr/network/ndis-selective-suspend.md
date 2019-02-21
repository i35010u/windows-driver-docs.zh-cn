---
title: NDIS 选择性挂起
description: NDIS 选择性挂起
ms.assetid: B0D44AE3-5197-4264-9838-83FB5EFEB0B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e487e400ccb97482ca7fa3adae88d03f20fc38f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519543"
---
# <a name="ndis-selective-suspend"></a>NDIS 选择性挂起


从开始 NDIS 6.30，NDIS 选择性挂起接口允许通过转换到低功耗状态适配器挂起空闲的网络适配器的 NDIS。 这使系统来减少开销上 CPU 和网络适配器的电源。

本部分包括以下主题：

[概述 NDIS 选择性挂起](overview-of-ndis-selective-suspend.md)

[报告 NDIS 选择性挂起功能](reporting-ndis-selective-suspend-capabilities.md)

[注册 NDIS 选择性挂起的处理程序函数](registering-ndis-selective-suspend-handler-functions.md)

[NDIS 选择性挂起空闲通知](ndis-selective-suspend-idle-notifications.md)

[标准化的 INF 关键字 ndis 选择性挂起](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NDIS 选择性挂起实施准则](ndis-selective-suspend-implementation-guidelines.md)

**请注意**  尽管 NDIS 选择性挂起接口是特别有用的 USB 网络适配器，该接口与总线无关。 因此，微型端口驱动程序可用于接口以便减少 CPU 和开销电源其他总线类型上的网络适配器。

 

 

 





