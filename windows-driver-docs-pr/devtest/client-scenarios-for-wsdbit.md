---
title: WSDBIT 的客户端方案
description: WSDBIT 的客户端方案
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 408373625f59ac92e9c80b549ebc57c8a1523d6e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803589"
---
# <a name="client-scenarios-for-wsdbit"></a>WSDBIT 的客户端方案


所有测试方案都是从客户端的角度来决定的。 在有限的情况下，完成该方案需要设备交互。 此要求在各自的方案中指示。

除非另有说明，否则假设测试设备 (TestDevice) 已启动，且在运行这些方案的网络段上可用。

某些方案定义了客户端与 TestDevice 中的 (一个或多个托管服务) 的客户端之间的交互。

客户端可以通过以下两种方式之一获取托管服务终结点

-   承载的服务终结点可以由用户提供。 这意味着，在 TestDevice 开始后，终结点已知，并可将其提供给正在运行客户端的参与方。

-   可以动态发现托管服务终结点。 这种情况意味着发现 TestDevice。 可以通过以下操作来发现 TestDevice：

    -   一个 Hello (，假定它是从设备启动的，并且有一个 **XAddrs** 字段) 。
    -   探测 \\ 解析交换。
    -   解析消息 (假定设备终结点的 *urn： uuid* 地址) 已知。

    然后，可以请求元数据，并随后检查 HostedService 元数据将显示端点。

客户端可以选择支持其中任一方法，但 TestDevice 必须支持这两种方法才能获得托管服务终结点。

客户端必须能够验证从 TestDevice 接收的附件。 应通过将预期的附件的副本加载到内存中，并对收到的附件执行字节的内存比较来验证附件。

当客户端发送事件的续订时，他们可以选择手动启动续订，或在原始 SubscribeResponse 消息中指定的续订期的一半结束后自动发送续订。

**注意**   因为测试用例可能会依赖于先前测试用例的结果，所以应按顺序运行测试用例。  (例如，1.3.8 取决于1.2.1 的结果。 ) 测试方案之间没有依赖关系 (例如，在事件和附件方案) 之间没有依赖关系。 第一种方案 (设备和服务检测) 的所有高级方案存在隐式依赖关系，因为未能发现 TestDevice 并检查其托管服务将阻止执行特定的高级方案。

 

本节包括下列主题：

[设备和服务检查方案](device-and-service-inspection-scenarios.md)

[设备控制方案](device-control-scenarios.md)

[附件方案](attachments-scenarios.md)

[事件方案](eventing-scenarios.md)

[安全通信方案](secure-communication-scenarios.md)

 

 





