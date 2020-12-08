---
title: 设备控制方案
description: 设备控制方案
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 设备控制方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95bb346c0fd97134b05323f82018bf79a12d3926
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783321"
---
# <a name="device-control-scenarios"></a>设备控制方案


设备控制方案测试简单的 SOAP 消息交换。

此方案的目标是不会发现所承载的服务终结点。 此方案假定在此方案之前发现或提供了这些终结点。 对于这种情况，必须在物理网络上对这些终结点寻址。 有关详细信息，请参阅 [WSDBIT 测试环境](wsdbit-testing-environment.md)中的初始测试设备安装程序关系图。

Case Client action Server action Pass-Fail 条件 **2.1**

**单向方法**

2.1.1

调用 SimpleService 的 **单向** 方法：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/OneWay**

-   \/将使用 http：/testdevice.interop/SimpleService1 服务。

-   提供整数输入。

显示从 **单向** 方法接收的整数。

发送的整数是显示的整数。

**2.2**

**双向方法**

2.2.1

调用 SimpleService 的 **双向** 方法：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/TwoWayRequest**

-   \/将使用 http：/testdevice.interop/SimpleService1 服务。

-   提供了两个整数输入。

通过将 **TwoWayResponse** 方法与结合使用来响应客户端：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/TwoWayResponse**

-   Sum 参数是从两个输入参数的总和计算得出的。

客户端收到的 sum 参数确实是在 **双向** 方法中发送的整数值的总和。

**2.3**

**TypeCheck 方法**

2.3.1

调用 SimpleService 的 **TypeCheck** 方法：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/TypeCheckRequest**

-   \/将使用 http：/testdevice.interop/SimpleService1 服务。

-   提供了 **xs： anyURI** 参数的 boolean、decimal、float 和 list。

通过将 **TypeCheckResponse** 方法与结合使用来响应客户端：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/TypeCheckResponse**

-   返回 **xs： anyURI** 参数的 boolean、decimal、float 和 list，并回显到客户端。

在将设备回送到客户端之前，在设备上正确显示了 **xs： anyURI** 参数的布尔值、decimal、float 和 list。 在客户端接收参数时，它们会再次正确显示。

**2.4**

**AnyCheck 方法**

2.4.1

调用 SimpleService 的 **AnyCheck** 方法：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/AnyCheckRequest**

-   \/将使用 http：/testdevice.interop/SimpleService1 服务

-   任意 XML 片段用作参数。

通过将 **TypeCheckResponse** 方法与结合使用来响应客户端：

-   **wsa： Action = = http： \/ /schemas.example.org/SimpleService/AnyCheckResponse**

-   返回任意 XML 片段并回显到客户端。

向客户端回送到客户端之前，从客户端发送的 XML 片段会正确显示在设备上。 当在客户端收到 XML 片段时，它会再次正确显示。

 

 

 





