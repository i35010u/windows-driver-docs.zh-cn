---
title: NDIS 选择性挂起空闲通知概述
description: NDIS 选择性挂起空闲通知概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4feae237140a87c2db57dfd1abd113a24cfc0e4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801533"
---
# <a name="overview-of-ndis-selective-suspend-idle-notifications"></a>NDIS 选择性挂起空闲通知概述


当微型端口驱动程序已启用并注册 NDIS 选择性挂起支持时，NDIS 会监视基础网络适配器的 i/o 活动。 如果 NDIS 确定驱动程序和适配器处于空闲状态，NDIS 将执行选择性挂起操作。 此操作通过将适配器转换为低功耗状态来挂起网络适配器。

NDIS 通过向微型端口驱动程序发出空闲通知来启动选择性挂起操作。 如果网络适配器在低功耗状态下处于挂起状态，则只有在取消空闲通知时，适配器才能恢复到完全电源状态。 在取消通知并且适配器处于全电源状态后，选择性挂起操作完成。

以下主题提供了有关 NDIS 选择性挂起操作和空闲通知的详细信息：

[NDIS 如何检测空闲的网络适配器](how-ndis-detects-idle-network-adapters.md)

[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)

[取消 NDIS 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)

[完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)

 

 





