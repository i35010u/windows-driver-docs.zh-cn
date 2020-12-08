---
title: 事件方案
description: 事件方案
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 事件方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cde1497942854ace4ca2d5fb15dd6cc9afc9394
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784047"
---
# <a name="eventing-scenarios"></a>事件方案

事件方案测试事件（如 [Web 服务的设备配置文件 ](https://docs.oasis-open.org/ws-dd/ns/dpws/2009/01)中的约束） (DPWS) 。

此方案的目标是不会发现所承载的服务终结点。 此方案假定在开始此方案之前发现或提供了这些终结点。

在这些情况下，NotifyTo 和 EndTo 地址格式应为物理地址，而不应为类型 **uuid： f014e8aa-fc6a-49f5-b862-1e53663a85ff** 的虚拟地址。

有关详细信息，请参阅 [WSDBIT 测试环境](wsdbit-testing-environment.md)中的初始测试设备安装程序关系图。

|案例|客户端操作|服务器操作|Pass-Fail 条件|
|----|----|----|----|
|**4.1**|**事件的订阅和续订。**| | |
|4.1.1|订阅 SimpleEvent：</br>- `wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"`</br>- `wse:Filter == http://schemas.example.org/EventingService/SimpleEvent`</br>客户端可以包括类型为 **xs： duration** 的过期时间。|发送有效期足以完成步骤4.1.2 的 SubscribeResponse。 过期时间必须是 **xs： duration** 类型。</br>对于此测试，服务器不需要使用从客户端请求的相同 **xs： duration** 。|客户端接收响应，并可跳到步骤4.1.2。|
|4.1.2|无|激发 SimpleEvent。|在客户端接收到事件。|
|4.1.3|将续订发送到 SimpleEvent。</br>当客户端发送事件的续订时，他们可以选择手动启动续订，或在原始 SubscribeResponse 消息中指定的续订期的一半时间已过时自动发送续订。|发送有效期长度足以完成步骤4.1.4 的 RenewResponse。 过期时间必须是 **xs： duration** 类型。|响应会在客户端接收，并可跳到步骤4.1.4。|
|4.1.4|无|激发 SimpleEvent。|在客户端接收到事件。|
|4.1.5|将取消订阅发送到 SimpleEvent 的 TestDevice。|发送 UnsubscribeResponse。|客户端接收响应，可以前往步骤4.1.6。|
|4.1.6|无|激发 SimpleEvent。|不会在客户端收到事件。|
|**4.2**|**具有 expiries 的订阅**| | |
|4.2.1|使用过期订阅订阅 SimpleEvent：</br>- `wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"`</br>- `wse:Filter == http://schemas.example.org/EventingService/SimpleEvent`</br>-过期持续时间必须足够长，才能完成步骤4.2.2。 过期时间必须为 **xs： duration**。</br>wsdbit \_ 客户端使用60分钟作为持续时间。|向发送 SubscribeResponse：</br>-在订阅请求中发送的过期时间将在 SubscribeResponse 中返回。|客户端接收具有正确过期的响应，并可执行步骤4.2.2。|
|4.2.2|无|激发 SimpleEvent。|客户端接收到事件。|
|4.2.3|对于其 SimpleEvent 订阅，将续订，其中包含过期时间到 TestDevice。 过期持续时间必须足够长，才能完成步骤4.2.4。 过期时间必须为 **xs： duration**。</br>当客户端发送事件的续订时，他们可以选择手动启动续订，或在原始 SubscribeResponse 消息中指定的续订期的一半时间已过时自动发送续订。|向发送 RenewResponse：</br>-在 RenewResponse 中返回续订请求中发送的过期时间。|客户端接收具有正确过期的响应，并可执行步骤4.2.4。|
|4.2.4|无|激发 SimpleEvent。|客户端接收到事件。|
|**4.3**|**多个事件源的订阅、续订和 expiries**| | |
|4.3.1|订阅 SimpleEvent</br>- `wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"`</br>- `wse:Filter == http://schemas.example.org/EventingService/SimpleEvent`</br>客户端可以选择包括 " **xs： duration**" 类型的过期时间。|发送有效期长度足以完成步骤4.3.3 的 SubscribeResponse。 过期时间必须是 xs： duration 类型。</br>对于此测试，服务器不需要使用从客户端请求的相同 **xs： duration** 。|客户端接收响应，可以执行步骤4.3.3。|
|4.3.2|订阅 SimpleEvent：</br>- `wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"`</br>- `wse:Filter == http://schemas.example.org/EventingService/IntegerEvent`</br>客户端可以选择包括 " **xs： duration**" 类型的过期时间。|发送有效期长度足以完成步骤4.3.4 的 SubscribeResponse。 过期时间必须是 **xs： duration** 类型。</br>对于此测试，服务器不需要使用从客户端请求的相同 **xs： duration** 。|客户端接收响应，可以执行步骤4.3.4。|
|4.3.3|无|激发 SimpleEvent。|客户端接收到事件。|
|4.3.4|无|激发 IntegerEvent。|在客户端接收事件，并显示正确的整数。|
|4.3.5|将续订发送到 IntegerEvent。</br>当客户端发送事件的续订时，他们可以选择手动启动续订，或在原始 SubscribeResponse 消息中指定的续订期的一半时间已过时自动发送续订。|发送有效期长度足以完成步骤4.3.8 的 RenewResponse。 过期时间必须是 **xs： duration** 类型。|在客户端接收响应。|
|4.3.6|将取消订阅发送到 SimpleEvent 的 TestDevice。|发送 UnsubscribeResponse。|客户端接收响应，可以前往步骤4.3.7。|
|4.3.7|无|激发 SimpleEvent。|不会在客户端收到事件。|
|4.3.8|无|激发 IntegerEvent。|在客户端接收事件，并显示正确的整数。|
|4.3.9|将取消订阅发送到 IntegerEvent 的 TestDevice。|发送 UnsubscribeResponse。|客户端接收响应，可以前往步骤4.3.10。|
|4.3.10|无|激发 IntegerEvent。|不会在客户端收到事件。|
|**4.4**|**订阅失败和故障**| | |
|4.4.1|订阅 FaultingEvent：</br>- `wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"`</br>- `wse:Filter == http://schemas.example.org/EventingService/FaultingEvent`|由于不支持此事件，因此必须发送 **wsdp： FilterActionNotSupported** SOAP 错误。|在客户端观察到订阅失败。|
