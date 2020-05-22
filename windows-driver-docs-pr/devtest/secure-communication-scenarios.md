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
ms.openlocfilehash: ee9220c9d8634fa4f4209afe473d5d1fc01aa18e
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769675"
---
# <a name="secure-communication-scenarios"></a>安全通信方案


安全通信方案使用安全通道测试发现、元数据交换和事件。

在尝试这些方案之前，应已成功完成[设备和服务检查](device-and-service-inspection-scenarios.md)以及[事件](eventing-scenarios.md)方案。

若要详细了解常规 WSDAPI 规范的符合性，请参阅[WSDAPI 规范符合性](https://docs.microsoft.com/windows/win32/wsdapi/wsdapi-specification-compliance)。

案例客户端操作服务器操作传递-失败条件**5.1**

**为安全设备调用探测**

5.1.1

使用发送通配符探测器

-   使用默认匹配规则。

-   无**wsd： Types**元素。

-   无**wsd：范围**元素。

使用 ProbeMatches 响应。

**注意**   如果提供了**wsd： XAddrs** ，则此地址必须为 https URI， **wsa： EndpointReference/wsa： address**必须与**wsd： XAddrs**相同。

 

请参阅步骤5.1.2 （或5.1.3）。

5.1.2 \[ 可选

仅当 ProbeMatches 中不提供 wsd： XAddrs 时，才需要执行此步骤\]

将解析发送到在 ProbeMatches 中指定的**wsa： EndpointReference/wsa： Address** 。

使用 ResolveMatches 响应。

**注意**   **Wsd： XAddrs**必须是 https URI， **wsa： EndpointReference/wsa： Address**必须与**wsd： XAddrs**相同。

 

请参阅步骤5.1.3。

5.1.3

将 GetMetadataRequest 发送到 TestDevice。

使用 GetMetadataResponse 响应。

请参阅步骤5.1.4。

5.1.4

显示 ThisDevice 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

5.1.5

显示 ThisModel 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

5.1.6

显示主机，HostedService，EndpointReference。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

**5.2**

**定向探测到安全设备**

5.2.1

发送通配符探测作为 HTTPS 请求，使用：

-   使用默认匹配规则。

-   无 wsd： Types 元素

-   无 wsd：范围元素

-   提供 HTTP 地址。

使用 HTTPS 响应响应 ProbeMatches。

**注意**   如果提供了**wsd： XAddrs** ，则此地址必须为 https URI， **wsa： EndpointReference/wsa： address**必须与**wsd： XAddrs**相同。

 

确认 TestDevice 的**wsa： EndpointReference/wsa： Address**正确。

**5.3**

**将事件订阅和续订到安全设备**

安全设备的发现通过使用在5.1 或5.2 中测试的方法来确定。

5.3.1

订阅 SimpleEvent：

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse： Filter = =http://schemas.example.org/EventingService/SimpleEvent**

客户端可以选择包括 " **xs： duration**" 类型的过期时间。

发送有效期长度足以完成步骤5.3.2 的 SubscribeResponse。 过期时间必须是**xs： duration**类型。

对于此测试，服务器不需要使用从客户端请求的相同**xs： duration** 。

客户端接收响应，可以执行步骤5.3.2。

5.3.2

Nothing

激发 SimpleEvent。

在客户端接收到事件。

5.3.3

将续订发送到 SimpleEvent。

当客户端发送事件的续订时，他们可以选择手动启动续订，或在原始 SubscribeResponse 消息中指定的续订期的一半时间已过时自动发送续订。

发送有效期长度足以完成步骤5.3.4 的 RenewResponse。 过期时间必须是**xs： duration**类型。

响应会在客户端接收，并可跳到步骤5.3.4。

5.3.4

Nothing

激发 SimpleEvent。

在客户端接收到事件。

5.3.5

将取消订阅发送到 SimpleEvent 的 TestDevice。

发送 UnsubscribeResponse。

客户端接收响应，可以前往步骤5.3.6。

5.3.6

Nothing

激发 SimpleEvent。

不会在客户端收到事件。

 

 

 





