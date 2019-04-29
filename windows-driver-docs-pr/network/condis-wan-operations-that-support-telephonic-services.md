---
title: 支持电话服务的 CoNDIS WAN 操作
description: 支持电话服务的 CoNDIS WAN 操作
ms.assetid: 698d7667-8620-4f98-aa57-e48195f612e3
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络连接、 台电话服务
- WDK WAN 台电话服务
- NDPROXY WDK 网络
- CoNDIS TAPI WDK 网络
- 有关台电话服务 WDK WAN 的台电话服务。
- WAN 微型端口驱动程序 WDK 网络连接、 台电话服务
- TAPI WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40eac07481ea4ba12824b8974c425556080508f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390730"
---
# <a name="condis-wan-operations-that-support-telephonic-services"></a>支持电话服务的 CoNDIS WAN 操作





本部分介绍的 CoNDIS WAN 微型端口驱动程序如何实现在面向连接的环境中使用 NDIS 函数台电话服务。 WAN 的 CoNDIS 微型端口驱动程序通过 NDIS NDPROXY 和 NDISWAN 驱动程序进行通信。 NDPROXY 驱动程序与通过电话服务提供商的电话服务应用程序进行通信。 有关详细信息，请参阅电话服务应用程序编程接口 (TAPI) Microsoft Windows SDK 文档中。

下面的主题更全面介绍 NDPROXY 驱动程序。 这些主题还介绍了的 CoNDIS WAN 的微型端口驱动程序注册和功能、 如何此时将显示行，以及如何设置了枚举其 TAPI 并关闭由 TAPI 请求启动的调用：

[NDPROXY 概述](ndproxy-overview.md)

[CoNDIS TAPI 注册](condis-tapi-registration.md)

[CoNDIS TAPI 初始化](condis-tapi-initialization.md)

[使传出调用](making-outgoing-calls.md)

[接受传入的调用](accepting-incoming-calls.md)

[CoNDIS TAPI 关闭](condis-tapi-shutdown.md)

[为语音流调用管理器要求](call-manager-requirements-for-voice-streaming.md)

[非 WAN 特定扩展，以支持通过面向连接的 NDIS 台电话服务](non-wan-specific-extensions-to-support-telephonic-services-over-connec.md)

这些说明将简要介绍 TAPI 中, 体现的概念，但，读者应当阅读 Windows SDK TAPI 有关的详细信息。 详细了解如何为 TAPI 模型的线路设备及如何所有 WAN 微型端口驱动程序应保留其连接的状态，请参阅[线路设备、 地址和调用 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff549181)和[维护状态信息 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff549232)。

 

 





