---
title: WAN 的 CoNDIS 是更加灵活
description: WAN 的 CoNDIS 是更加灵活
ms.assetid: 01f4d5cc-3ecc-4d2f-bc19-67b8d0fda52f
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络权益
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f6747502d3fbbcb2df0042f3523addd5fad2d92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555040"
---
# <a name="condis-wan-is-more-flexible"></a>WAN 的 CoNDIS 是更加灵活





在的 CoNDIS 模型中，主要功能 （如调用管理和数据传输） 被划分到离散组件或子组件。 此组织，可使用系统提供和第三方组件并更轻松地更新功能。

CoNDIS 模型提供了四种类型的驱动程序：

-   面向连接的客户端驱动程序

-   调用管理器

-   面向连接的微型端口驱动程序

-   集成的微型端口调用管理器 (MCMs)

有关的 CoNDIS 驱动程序的详细信息，请参阅[Connection-Oriented NDIS](connection-oriented-ndis.md)。

呼叫管理器和微型端口驱动程序组件分离，可更新的微型端口驱动程序来支持新硬件，而呼叫管理器将保持不变。 在许多情况下，呼叫管理器可能需要升级仅以更正缺陷。

分离的体系结构组件保持在 MCM 中明确定义。 MCM 的调用管理器子组件处理的信号方面的连接，而 CoNDIS WAN 的微型端口驱动程序子组件处理 NIC 硬件。

可以使用系统提供呼叫管理器。 如果你的媒体类型 （与一样，例如，ISDN)，系统不提供呼叫管理器，可以编写一个，也可以有可能获得一个第三方。

Microsoft Windows 操作系统包括的 CoNDIS PPP 客户端和 WAN 的 CoNDIS 微型端口驱动程序是可用于多个设备。 您可以编写的 CoNDIS WAN 的客户端来扩展系统以支持除了 PPP 其他协议驱动程序。

WAN 的 CoNDIS 模型并不限于 PPP 数据。 您可以实现自定义 WAN 的客户端驱动程序和微型端口驱动程序来处理，例如，原始数据进行流式处理或专有加密。

 

 





