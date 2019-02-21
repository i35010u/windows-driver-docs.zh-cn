---
title: NDIS 选择性挂起空闲通知
description: NDIS 选择性挂起空闲通知
ms.assetid: 958A2588-A847-4699-9906-95FB47CA1CDC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e6759c3617c1bf5342bd3eae75e1df3baa16f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545625"
---
# <a name="ndis-selective-suspend-idle-notifications"></a>NDIS 选择性挂起空闲通知


当微型端口驱动程序已启用并注册支持 NDIS 选择性挂起，NDIS 监视的基础网络适配器的 I/O 活动。 如果 NDIS 确定驱动程序和适配器处于空闲状态，NDIS 执行选择性挂起操作。 此操作通过转换到低功耗状态适配器将挂起的网络适配器。

NDIS 启动选择性挂起操作通过向微型端口驱动程序发出的空闲通知。 当在低功耗状态中挂起时的网络适配器时，适配器可以空闲通知被取消时，仅恢复到全功率状态。 已取消通知并适配器处于全功率状态后，选择性挂起操作完成。

以下主题提供有关详细信息的 NDIS 选择性挂起操作和空闲通知：

[NDIS 如何检测空闲的网络适配器](how-ndis-detects-idle-network-adapters.md)

[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)

[正在取消 NDIS 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)

[完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)

 

 





