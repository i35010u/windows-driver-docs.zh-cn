---
title: 支持电话服务的 CoNDIS WAN 操作
description: 支持电话服务的 CoNDIS WAN 操作
ms.assetid: 698d7667-8620-4f98-aa57-e48195f612e3
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，telephonic 服务
- telephonic services WDK WAN
- NDPROXY WDK 网络
- CoNDIS TAPI WDK 网络
- telephonic services WDK WAN，关于 telephonic 服务
- WAN 微型端口驱动程序 WDK 网络，telephonic 服务
- TAPI WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a007c0404b5479baca9f1563a4af4a1fdd2ee78f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206763"
---
# <a name="condis-wan-operations-that-support-telephonic-services"></a>支持电话服务的 CoNDIS WAN 操作





本部分介绍 CoNDIS WAN 微型端口驱动程序如何在面向连接的环境中使用 NDIS 函数实现 telephonic 服务。 CoNDIS WAN 微型端口驱动程序通过使用 NDPROXY 和 NDISWAN 驱动程序的 NDIS 进行通信。 NDPROXY 驱动程序通过电话服务提供程序与电话服务应用程序通信。 有关详细信息，请参阅 Microsoft Windows SDK 文档中 (TAPI) 的电话应用程序编程接口。

以下主题更全面地描述了 NDPROXY 驱动程序。 这些主题还介绍了 CoNDIS WAN 微型端口驱动程序如何注册和枚举其 TAPI 功能，如何提供线路，以及它如何设置和关闭由 TAPI 请求启动的调用：

[NDPROXY 概述](ndproxy-overview.md)

[CoNDIS TAPI 注册](condis-tapi-registration.md)

[CoNDIS TAPI 初始化](condis-tapi-initialization.md)

[拨打电话](making-outgoing-calls.md)

[接受来电](accepting-incoming-calls.md)

[CoNDIS TAPI 关闭](condis-tapi-shutdown.md)

[语音流的呼叫管理程序要求](call-manager-requirements-for-voice-streaming.md)

[用于通过面向连接的 NDIS 支持电话服务的非 WAN 特定扩展](non-wan-specific-extensions-to-support-telephonic-services-over-connec.md)

这些说明简要介绍了 TAPI 中所述的概念，但读者应该参考 Windows SDK 获取有关 TAPI 的详细信息。 有关 TAPI 如何对设备以及所有 WAN 微型端口驱动程序如何维护其连接状态的详细信息，请参阅 [线路设备、地址和调用 (ndis 5.1) ](/previous-versions/windows/hardware/network/ff549181(v=vs.85)) 和 [ (Ndis 5.1) 维护状态信息 ](/previous-versions/windows/hardware/network/ff549232(v=vs.85))。

 

