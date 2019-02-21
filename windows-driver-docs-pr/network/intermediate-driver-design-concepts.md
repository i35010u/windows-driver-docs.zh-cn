---
title: 中间驱动程序设计概念
description: 中间驱动程序设计概念
ms.assetid: cee13268-5df0-4d71-a115-3168c56be06c
keywords:
- 中间驱动程序 WDK 网络、 写入
- NDIS 中间驱动程序 WDK、 写入
- 编写 NDIS 中间驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fae498f7fd0b4ac3c6e025b32f95e1df192ec3ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519462"
---
# <a name="intermediate-driver-design-concepts"></a>中间驱动程序设计概念





本部分提供一些基本信息以帮助你开始编写 NDIS 中间驱动程序。 若要编写 NDIS 中间层驱动程序，必须了解的 NDIS 微型端口驱动程序和协议驱动程序操作和函数。

MUX 中间驱动程序示例中 Microsoft Windows Driver Kit (WDK) 提供的基本示例*n*-到-一个 MUX 中间驱动程序，你可以调整以适应你的特定需求。

NDIS 中间驱动程序的虚拟微型端口必须反序列化。 *反序列化的驱动程序*序列化其自己的操作*MiniportXxx*函数和内部所有传入的队列发送网络数据，而不是依靠 NDIS 以执行这些操作。 此操作会导致全双工性能明显优于，如果驱动程序的关键部分 （一次只有一个线程可以执行的代码） 进行较小。 有关反序列化的驱动程序的详细信息，请参阅[反序列化的 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

NDIS 中间驱动程序可以支持在其虚拟微型端口仅限于无连接的通信。 在其协议接口，但是，NDIS 中间驱动程序可以支持无连接的通信或面向连接的通信。 有关面向连接的通信的详细信息，请参阅[Connection-Oriented NDIS](connection-oriented-ndis.md)。

一个或多个 NDIS 微型端口驱动程序上方和下方的传输驱动程序，通常是分层结构中间的驱动程序。 此外可以与其他中间驱动程序分层中间驱动程序。

以下主题提供有关编写中间的 NDIS 驱动程序的其他信息：

[DriverEntry 中间驱动程序函数](intermediate-driver-driverentry-function.md)

[中间的驱动程序中动态绑定](dynamic-binding-in-an-intermediate-driver.md)

[中间驱动程序查询和集合操作](intermediate-driver-query-and-set-operations.md)

[中间驱动程序网络数据管理](intermediate-driver-network-data-management.md)

[在中间的驱动程序中接收数据](receiving-data-in-an-intermediate-driver.md)

[通过中间驱动程序的网络数据传输](transmitting-network-data-through-an-intermediate-driver.md)

[处理即插即用事件和中间驱动程序中的电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)

[中间驱动程序重置操作](intermediate-driver-reset-operations.md)

[状态指示中间驱动程序中](status-indications-in-an-intermediate-driver.md)

 

 





