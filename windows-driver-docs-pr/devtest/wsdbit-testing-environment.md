---
title: WSDBIT 测试环境
description: WSDBIT 测试环境
ms.assetid: 6fa6f6f7-859a-4424-a71d-600f82b23f89
keywords:
- WSDBIT 工具 WDK，测试环境
- WSDAPI 基本互操作性工具 WDK，测试环境
- WSDBIT 工具 WDK，网络拓扑
- WSDAPI 基本互操作性工具 WDK，网络拓扑
- 测试环境 WDK WSDBIT
- WSDBIT 工具 WDK，服务
- WSDAPI 基本互操作性工具 WDK，服务
- SimpleService 服务 WDK WSDBIT
- AttachmentService 服务 WDK WSDBIT
- EventingService 服务 WDK WSDBIT
- WSDBIT 工具 WDK，用于测试的设备
- WSDAPI 基本互操作性工具 WDK、用于测试的设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c7aac8738f9a687cbce79e35721290089bb873c
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769669"
---
# <a name="wsdbit-testing-environment"></a>WSDBIT 测试环境


本主题介绍物理环境和设备及其托管服务功能。

### <a name="span-idnetwork_modelspanspan-idnetwork_modelspannetwork-model"></a><span id="network_model"></span><span id="NETWORK_MODEL"></span>网络模型

要测试的设备和客户端连接到以太网网段，并构成单个 IP 子网。 网络寻址方案（如 IPv4、IPv6 或主机名）并不相关，只要客户端和设备至少支持一个公用的方案，子网中必须只有一个设备和一个客户端。

为了便于调试和故障排除，你应该使用网络监视器来监视设备与客户端之间的流量交换。 若要监视所有流量，必须将设备和客户端通过以太网集线器连接到网段。 如果某个集线器不可用，则可以通过在运行 WSDBIT 的计算机上安装网络监视器来监视流量。

下图显示了由设备、客户端和网络监视器组成的网络拓扑，它们都是通过集线器连接的。

![阐释 wsdapi 基本互操作性工具（wsdbit）测试的网络拓扑的示意图](images/wsdbit1.png)

### <a name="span-idtest_devicespanspan-idtest_devicespantest-device"></a><span id="test_device"></span><span id="TEST_DEVICE"></span>测试设备

若要参与设备端测试，应按照以下一般准则所述来实现设备。 有关设备实现的详细信息，请参阅[WSDBIT Reference](wsdbit-reference.md)和[Web Services 的设备配置文件（DPWS）](http://schemas.xmlsoap.org/ws/2006/02/devprof/)规范。

下表描述了服务和互操作性测试用例依赖关系。

方案 SimpleService AttachmentService EventingService 设备和服务检查

一个或多个 SimpleService、AttachmentService 或 EventingService

设备控制

X

Attachments

X

事件处理

X

 

测试设备应托管三种类型的服务：

-   http://schemas.example.org/SimpleService

-   http://schemas.example.org/AttachmentService

-   http://schemas.example.org/EventingService

### <a name="span-idsimpleservicespanspan-idsimpleservicespansimpleservice"></a><span id="simpleservice"></span><span id="SIMPLESERVICE"></span>SimpleService

**SimpleService**服务有四种方法：

-   **单向**方法是将整数作为参数的单向方法。

-   **双向**是请求-响应方法，其中两个整数在请求中，并在响应中包含这些整数的总和。

-   **TypeCheck**是请求-响应方法，其中有许多不同类型的请求和响应中的完全相同的类型，包括 boolean、decimal、Float 和 url 列表。

-   **AnyCheck**是请求-响应方法，其中包含请求中的 XML 片段，并在响应中返回同一个片段。

### <a name="span-idattachmentservicespanspan-idattachmentservicespanattachmentservice"></a><span id="attachmentservice"></span><span id="ATTACHMENTSERVICE"></span>AttachmentService

**AttachmentService**服务发送和接收附件。 要发送和接收的附件数据在 \\ 互操作目录中包含为两个单独的文件： Image1 和 Image2。 此服务有两种方法：

-   **OneWayAttachment**是一种单向方法，其中附件作为参数。

-   **TwoWayAttachment**是一个请求-响应方法，其中包含请求和响应中的附件。

### <a name="span-ideventingservicespanspan-ideventingservicespaneventingservice"></a><span id="eventingservice"></span><span id="EVENTINGSERVICE"></span>EventingService

**EventingService**服务有两种可订阅的事件：

-   **SimpleEvent**是没有参数的事件。

-   **IntegerEvent**是返回整数的事件。

### <a name="span-idimplementing_test_servicesspanspan-idimplementing_test_servicesspanimplementing-test-services"></a><span id="implementing_test_services"></span><span id="IMPLEMENTING_TEST_SERVICES"></span>实现测试服务

若要执行所有互操作性测试事例，必须实现所有这些服务。 在这种情况下，在初始启动后，设备会承载其中每个服务的一个实例。

但是，如果你只想实现其中部分服务，请参阅本主题开头处的表，获取有关服务和互操作测试用例依赖项的信息。

**注意**   若要尝试任何高级互操作方案（如[设备控制](device-control-scenarios.md)、[附件](attachments-scenarios.md)和[事件](eventing-scenarios.md)），测试设备至少必须支持[设备和服务检查测试事例](device-and-service-inspection-scenarios.md)。 如果设备未通过该测试用例，则你可能无法继续高级测试用例。

 

测试设备和 WSDBIT 设备（WSDBIT \_ 服务器）必须能够执行以下操作：

-   显示**SimpleService**单向方法的整数输入参数。

-   显示在双向类型检查请求中提交的类型的值。

-   验证收到的附件是否与预期的已知附件有关，并且必须显示此验证的结果。

-   启动**EventingService**到手动输入或计时器中描述的两种事件。

-   显示在可扩展（**xs： any**）节中接收的数据。

-   使用**xs： anyURI testdevice**作为用于发现的**wsd： scope**元素。

 

 





