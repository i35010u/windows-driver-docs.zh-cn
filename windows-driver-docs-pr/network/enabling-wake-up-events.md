---
title: 启用唤醒事件
description: 启用唤醒事件
ms.assetid: 48ed0f41-efa0-4040-8589-8d477c5ddd0e
keywords:
- 唤醒功能 WDK 网络，启用唤醒事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26ce831906fac95a70a85e24273609bbfce8c565
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372500"
---
# <a name="enabling-wake-up-events"></a>启用唤醒事件





协议驱动程序可以发送[OID\_PNP\_启用\_唤醒\_向上](https://msdn.microsoft.com/library/windows/hardware/ff569775)启用一个或多个网络适配器的唤醒功能请求。 NDIS 不会立即启用这些唤醒功能。 相反，NDIS 跟踪的唤醒功能已启用的协议驱动程序中，和之前的微型端口驱动程序转换为休眠状态中，将发送一个 OID\_PNP\_启用\_唤醒\_达启用适当的唤醒活动的微型端口驱动程序。 后微型端口驱动程序初始化的网络适配器，或微型端口驱动程序时它继续从低功耗状态时，必须禁用任何唤醒网络适配器设置的方法。

之前，微型端口驱动程序将转换为低功耗状态 (即 NDIS 发送微型端口驱动程序 OID 之前\_PNP\_设置\_电源请求)，NDIS 发送微型端口驱动程序 OID\_PNP\_启用\_唤醒\_请求来启用网络适配器的唤醒功能。

 

 





