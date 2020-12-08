---
title: CoNDIS WAN 更灵活
description: CoNDIS WAN 更灵活
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，优点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f794e92d5273bebd8e177f721d5d52bd5a5533c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840661"
---
# <a name="condis-wan-is-more-flexible"></a>CoNDIS WAN 更灵活





在 CoNDIS 模型中，主要功能 (例如，调用管理和数据传输) 会事关到不同的组件或子组件中。 此组织使你可以更轻松地使用系统提供的和第三方组件和更新功能。

CoNDIS 模型提供四种类型的驱动程序：

-   面向连接的客户端驱动程序

-   呼叫管理器

-   面向连接的微型端口驱动程序

-    (MCMs) 的集成微型端口呼叫管理器

有关 CoNDIS 驱动程序的详细信息，请参阅 [面向连接的 NDIS](connection-oriented-ndis.md)。

通过分离调用管理器和微型端口驱动程序组件，你可以更新微型端口驱动程序以支持新硬件，同时呼叫管理器保持不变。 在许多情况下，呼叫管理器可能只要求升级才能纠正缺陷。

在 MCM 中，体系结构组件的分离仍是明确定义的。 MCM 的 "呼叫管理器" 子组件处理连接的信号方面，CoNDIS WAN 微型端口驱动程序子组件处理 NIC 硬件。

您可以使用系统提供的调用管理器。 如果系统没有为媒体类型提供呼叫管理器 (例如，ISDN) ，你可以编写一个，或者可能从第三方获取一个呼叫管理器。

Microsoft Windows 操作系统包含一个 PPP CoNDIS 客户端，而 CoNDIS WAN 微型端口驱动程序可用于多个设备。 你可以编写 CoNDIS WAN 客户端来扩展系统，以支持除 PPP 之外的其他协议驱动程序。

CoNDIS WAN 型号并不局限于 PPP 数据。 可以实现自定义 WAN 客户端驱动程序和微型端口驱动程序来处理原始数据流式处理或专用加密。

 

 





