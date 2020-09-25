---
title: 中间驱动程序设计概念
description: 中间驱动程序设计概念
ms.assetid: cee13268-5df0-4d71-a115-3168c56be06c
keywords:
- 中级驱动程序，WDK 网络，写入
- NDIS 中间驱动程序 WDK，编写
- 编写 NDIS 中间驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf78c16e15d2750eac79066bf7399072f506572c
ms.sourcegitcommit: 29c2e6dd8a3de3c11822d990adf1edd774f8a136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91230037"
---
# <a name="intermediate-driver-design-concepts"></a>中间驱动程序设计概念





本部分提供一些基本信息，帮助你开始编写 NDIS 中间驱动程序。 若要编写 NDIS 中间驱动程序，必须了解 NDIS 微型端口驱动程序和协议驱动程序操作和功能。

Microsoft Windows 驱动程序工具包 (WDK) 中的 MUX 中间驱动程序示例提供了一个可适应特定需要的 *n*对一 MUX 中间驱动程序的基本示例。

必须反序列化 NDIS 中间驱动程序的虚拟小型端口。 *反序列化的驱动程序* 序列化其自己的 *MiniportXxx* 函数的操作，并在内部将所有传入的发送网络数据排队，而不是依赖 NDIS 来执行这些操作。 如果驱动程序的关键部分 (只能由一个线程执行的代码（) 会保持较小），则此操作可显著提高全双工性能。 有关反序列化驱动程序的详细信息，请参阅 [反序列化 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

NDIS 中间驱动程序只能在其虚拟小型端口上支持无连接通信。 但是，在其协议接口上，NDIS 中间驱动程序可以支持无连接通信或面向连接的通信。 有关面向连接的通信的详细信息，请参阅 [面向连接的 NDIS](connection-oriented-ndis.md)。

中间驱动程序通常在一个或多个 NDIS 微型端口驱动程序上，并且位于传输驱动程序的下面。 中间驱动程序还可以与其他中间驱动程序进行分层。

以下主题提供有关编写 NDIS 中间驱动程序的其他信息：

[中间驱动程序 DriverEntry 函数](intermediate-driver-driverentry-function.md)

[中间驱动程序中的动态绑定](dynamic-binding-in-an-intermediate-driver.md)

[中间驱动程序查询和设置操作](intermediate-driver-query-and-set-operations.md)

[中间驱动程序网络数据管理](intermediate-driver-network-data-management.md)

[在中间驱动程序中接收数据](receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-e.md)

[通过中间驱动程序传输网络数据](transmitting-network-data-through-an-intermediate-driver.md)

[在中间驱动程序中处理 PnP 事件和电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)

[中间驱动程序重置操作](intermediate-driver-reset-operations.md)

[中间驱动程序中的状态指示](status-indications-in-an-intermediate-driver.md)

 

 





