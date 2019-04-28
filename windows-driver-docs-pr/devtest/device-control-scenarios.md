---
title: 设备控制方案
description: 设备控制方案
ms.assetid: 9effc192-77ef-40fd-9ab6-564637019576
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 设备控制方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a23a22ab9de5580998f1bb990c479716dff1a7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341671"
---
# <a name="device-control-scenarios"></a>设备控制方案


设备控制方案测试简单 SOAP 消息交换。

此方案的目标不是承载的服务终结点的发现。 此方案假设已发现或在此方案之前提供这些终结点。 对于此方案中，这些终结点必须是可寻址物理网络上。 有关详细信息，请参阅中的初始测试设备安装程序关系图[WSDBIT 测试环境](wsdbit-testing-environment.md)。

本例中客户端操作服务器操作启用通过/失败条件**2.1**

**单向方法**

2.1.1

调用**OneWay**与 SimpleService 方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/OneWay**

-   http://testdevice.interop/SimpleService1将使用服务。

-   提供整数输入。

显示从收到的整数**OneWay**方法。

已发送的整数是显示的整数。

**2.2**

**TwoWay 方法**

2.2.1

调用**TwoWay**与 SimpleService 方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/TwoWayRequest**

-   http://testdevice.interop/SimpleService1将使用服务。

-   提供两个整数输入。

通过响应客户端**TwoWayResponse**方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/TwoWayResponse**

-   Sum 参数会计算从两个输入参数的总和。

客户端收到的总和参数实际上是发送的整数值的总和**TwoWay**方法。

**2.3**

**一次方法**

2.3.1

调用**一次**与 SimpleService 方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/TypeCheckRequest**

-   http://testdevice.interop/SimpleService1将使用服务。

-   一个布尔值，decimal、 float、 和的列表**xs: anyuri**提供参数。

通过响应客户端**TypeCheckResponse**方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/TypeCheckResponse**

-   一个布尔值，decimal、 float、 和的列表**xs: anyuri**参数返回并回显给客户端。

一个布尔值，decimal、 float、 和的列表**xs: anyuri**参数正确显示在设备上之前它们回显给客户端。 这些参数会再次显示在客户端接收正确。

**2.4**

**AnyCheck 方法**

2.4.1

调用**AnyCheck**与 SimpleService 方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/AnyCheckRequest**

-   http://testdevice.interop/SimpleService1将使用服务

-   任意 XML 片段用作参数。

通过响应客户端**TypeCheckResponse**方法：

-   **wsa:Action = = http://schemas.example.org/SimpleService/AnyCheckResponse**

-   返回任意 XML 片断并将其发送回客户端。

从客户端发送的 XML 片段是在设备上正确显示之前回显给客户端。 在客户端接收时，XML 片段是再次正确显示。

 

 

 





