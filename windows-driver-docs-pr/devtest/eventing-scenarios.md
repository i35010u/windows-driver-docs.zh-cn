---
title: 事件方案
description: 事件方案
ms.assetid: 6f7832ed-2b0b-4857-b47e-7db492a53855
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 事件处理方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3eaf46b6a30cdc2684a373b2c746c7d655ec174
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344785"
---
# <a name="eventing-scenarios"></a>事件方案


事件处理方案测试事件处理，因为中加以约束[设备配置文件的 Web 服务 (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)。

此方案的目标不是承载的服务终结点的发现。 此方案假定这些终结点已发现或提供此方案开始之前。

对于这些方案的目的，NotifyTo 和 EndTo 地址格式应为物理地址和类型的不是虚拟地址**uuid: f014e8aa-fc6a-49f5-b862-1e53663a85ff**。

有关详细信息，请参阅中的初始测试设备安装程序关系图[WSDBIT 测试环境](wsdbit-testing-environment.md)。

本例中客户端操作服务器操作启用通过/失败条件**4.1**

**订阅和续订事件。**

4.1.1

订阅与 SimpleEvent:

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

客户端可以包含类型的过期**xs: duration**。

发送完成步骤 4.1.2 SubscribeResponse 过期时间足够长的时间。 类型必须为到期**xs: duration**。

对于此测试，服务器不需要使用同一**xs: duration**从客户端的请求。

客户端接收响应，并可以转到步骤 4.1.2。

4.1.2

无

激发 SimpleEvent。

在客户端收到事件。

4.1.3

发送续订 SimpleEvent。

当客户端发送的事件的续订时，他们可以选择手动启动续订或自动将续订发送时的原始 SubscribeResponse 消息中指定的续订期间下半部分已过。

发送完成步骤 4.1.4 RenewResponse 过期时间足够长的时间。 类型必须为到期**xs: duration**。

响应在客户端收到并可以转到步骤 4.1.4。

4.1.4

无

激发 SimpleEvent。

在客户端收到事件。

4.1.5

将发送到 TestDevice SimpleEvent 用于取消订阅。

UnsubscribeResponse 发送。

客户端接收响应，并可以转到步骤 4.1.6。

4.1.6

无

激发 SimpleEvent。

在客户端接收不到任何事件。

**4.2**

**使用满的订阅**

4.2.1

订阅具有使用过期的 SimpleEvent:

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

- 过期持续时间必须足够长的时间来完成的步骤 4.2.2。 必须为到期**xs: duration**。

wsdbit\_客户端使用 60 分钟作为持续时间。

发送与 SubscribeResponse:

-   订阅请求中发送的过期时间是在 SubscribeResponse 中返回。

客户端接收的响应与正确的过期时间，并可以转到步骤 4.2.2。

4.2.2

无

激发 SimpleEvent。

客户端在收到事件。

4.2.3

为其 SimpleEvent 订阅到 TestDevice 发送续订其过期时间。 过期持续时间必须足够长的时间来完成的步骤 4.2.4。 必须为到期**xs: duration**。

当客户端发送的事件的续订时，他们可以选择手动启动续订或自动将续订发送时的原始 SubscribeResponse 消息中指定的续订期间下半部分已过。

发送与 RenewResponse:

-   RenewResponse 返回续订请求中发送的过期时间。

客户端接收响应时使用正确的过期时间，并可以转到步骤 4.2.4。

4.2.4

无

激发 SimpleEvent。

客户端在收到事件。

**4.3**

**订阅、 续订和满的多个事件源**

4.3.1

订阅与 SimpleEvent

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

客户端可以选择包含类型的过期**xs: duration**。

发送完成步骤 4.3.3 SubscribeResponse 过期时间足够长的时间。 过期时间必须为类型为 xs: duration。

对于此测试，服务器不需要使用同一**xs: duration**从客户端的请求。

客户端接收响应，并可以转到步骤 4.3.3。

4.3.2

订阅与 SimpleEvent:

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/IntegerEvent**

客户端可以选择包含类型的过期**xs: duration**。

发送完成步骤 4.3.4 SubscribeResponse 过期时间足够长的时间。 类型必须为到期**xs: duration**。

对于此测试，服务器不需要使用同一**xs: duration**从客户端的请求。

客户端接收响应，并可以转到步骤 4.3.4。

4.3.3

无

激发 SimpleEvent。

客户端在收到事件。

4.3.4

无

激发 IntegerEvent。

在客户端接收事件，并显示正确的整数。

4.3.5

发送续订 IntegerEvent。

当客户端发送的事件的续订时，他们可以选择手动启动续订或自动将续订发送时的原始 SubscribeResponse 消息中指定的续订期间下半部分已过。

发送完成步骤 4.3.8 RenewResponse 过期时间足够长的时间。 类型必须为到期**xs: duration**。

在客户端收到响应。

4.3.6

将发送到 TestDevice SimpleEvent 用于取消订阅。

UnsubscribeResponse 发送。

客户端接收响应，并可以转到步骤 4.3.7。

4.3.7

无

激发 SimpleEvent。

在客户端接收不到任何事件。

4.3.8

无

激发 IntegerEvent。

在客户端接收事件，并显示正确的整数。

4.3.9

将发送到 TestDevice IntegerEvent 用于取消订阅。

UnsubscribeResponse 发送。

客户端接收响应，并可以转到步骤 4.3.10。

4.3.10

无

激发 IntegerEvent。

在客户端接收不到任何事件。

**4.4**

**订阅失败和错误**

4.4.1

订阅与 FaultingEvent:

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/FaultingEvent**

由于不支持此事件， **wsdp:FilterActionNotSupported**必须发送 SOAP 错误。

未能订阅观察到在客户端。

 

 

 





