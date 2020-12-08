---
title: 启用唤醒事件
description: 启用唤醒事件
keywords:
- 唤醒功能 WDK 网络，启用唤醒事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11279bea9a87bc7cb01465e0edb7819c9561594f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823939"
---
# <a name="enabling-wake-up-events"></a>启用唤醒事件





协议驱动程序可以发送 [OID \_ PNP \_ enable \_ 唤醒 \_ ](./oid-pnp-enable-wake-up.md) 请求，以启用一个或多个网络适配器的唤醒功能。 NDIS 不会立即启用这些唤醒功能。 相反，NDIS 将跟踪由协议驱动程序启用的唤醒功能，并且在微型端口驱动程序转换为休眠状态之前，会将 OID \_ PNP \_ 启用启用 \_ \_ 到微型端口驱动程序的唤醒，以启用适当的唤醒事件。 当微型端口驱动程序初始化网络适配器，或从低功耗状态恢复后，微型端口驱动程序必须禁用网络适配器上设置的任何唤醒方法。

在微型端口驱动程序转换为低功耗状态之前 (也就是说，在 NDIS 向微端口驱动程序发送 OID \_ pnp \_ 集 \_ 电源请求) 之前，ndis 将发送微型端口驱动程序 oid \_ pnp \_ 启用 \_ 唤醒 \_ 请求，以启用网络适配器的唤醒功能。

 

