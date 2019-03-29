---
title: 安全通信方案
description: 安全通信方案
ms.assetid: 0273f4e7-0b93-4ab1-8564-e51c14e91243
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 安全通信方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c40b21e295c17d62e4f2894e4fe3b65dfb27fa47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568765"
---
# <a name="secure-communication-scenarios"></a>安全通信方案


通过使用安全通道，安全通信方案测试发现、 元数据交换和事件处理。

之前尝试这些方案，您应已成功完成[设备和服务检查](device-and-service-inspection-scenarios.md)并[Eventing](eventing-scenarios.md)方案。

在之前尝试这些互操作性测试用例，请参阅[使用安全通道使用 WSDAPI](https://go.microsoft.com/fwlink/p/?linkid=81271)并[配置 WSDAPI 应用程序以使用安全通道](https://go.microsoft.com/fwlink/p/?linkid=81272)有关安全通道的详细信息。

本例中客户端操作服务器操作启用通过/失败条件**5.1**

**安全设备的调用探测**

5.1.1

发送与通配符探测

-   使用默认的匹配规则。

-   否**wsd:Types**元素。

-   否**wsd:Scopes**元素。

使用 ProbeMatches 做出响应。

**请注意**  如果**wsd:XAddrs**是提供，该地址必须是 https URI 并**wsa: endpointreference / wsa： 地址**必须是与相同**wsd:XAddrs**。

 

转到步骤 5.1.2 （或 5.1.3）。

5.1.2\[可选

此步骤才是必需的如果没有 wsd:XAddrs 提供在 5.1.1 ProbeMatches 中\]

发送到解决**wsa: endpointreference / wsa： 地址**从 1.2.1 ProbeMatches 中指定。

使用 ResolveMatches 做出响应。

**请注意**   **wsd:XAddrs**必须是 https URI 并**wsa: endpointreference / wsa： 地址**必须是与相同**wsd:XAddrs**。

 

转到步骤 5.1.3。

5.1.3

发送到 TestDevice GetMetadataRequest。

使用 GetMetadataResponse 做出响应。

转到步骤 5.1.4。

5.1.4

显示 ThisDevice 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

5.1.5

显示 ThisModel 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

5.1.6

显示主机，托管服务，EndpointReference。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

**5.2**

**定向到安全设备探测**

5.2.1

发送包含通配符作为 HTTPS 探测请求：

-   使用默认的匹配规则。

-   没有 wsd:Types 元素

-   没有 wsd:Scopes 元素

-   提供的 HTTP 地址。

通过使用 HTTPS 响应 ProbeMatches 做出响应。

**请注意**  如果**wsd:XAddrs**是提供，该地址必须是 https URI 并**wsa: endpointreference / wsa： 地址**必须是与相同**wsd:XAddrs**。

 

确认**wsa: endpointreference / wsa： 地址**TestDevice 是正确。

**5.3**

**订阅和续订事件与安全设备**

使用在 5.1 或 5.2 中测试的方法来确定安全设备的发现。

5.3.1

订阅与 SimpleEvent:

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

客户端可以选择包含类型的过期**xs: duration**。

发送完成步骤 5.3.2 SubscribeResponse 过期时间足够长的时间。 类型必须为到期**xs: duration**。

对于此测试，服务器不需要使用同一**xs: duration**从客户端的请求。

客户端接收响应，并可以转到步骤 5.3.2。

5.3.2

无

激发 SimpleEvent。

在客户端收到事件。

5.3.3

发送续订 SimpleEvent。

当客户端发送的事件的续订时，他们可以选择手动启动续订或自动将续订发送时的原始 SubscribeResponse 消息中指定的续订期间下半部分已过。

发送完成步骤 5.3.4 RenewResponse 过期时间足够长的时间。 类型必须为到期**xs: duration**。

响应在客户端收到并可以转到步骤 5.3.4。

5.3.4

无

激发 SimpleEvent。

在客户端收到事件。

5.3.5

将发送到 TestDevice SimpleEvent 用于取消订阅。

UnsubscribeResponse 发送。

客户端接收响应，并可以转到步骤 5.3.6。

5.3.6

无

激发 SimpleEvent。

在客户端接收不到任何事件。

 

 

 





