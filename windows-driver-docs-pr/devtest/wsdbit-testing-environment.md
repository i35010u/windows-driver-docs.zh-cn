---
title: WSDBIT 测试环境
description: WSDBIT 测试环境
ms.assetid: 6fa6f6f7-859a-4424-a71d-600f82b23f89
keywords:
- WSDBIT 工具 WDK，测试环境
- WSDAPI 基本互操作性工具 WDK，测试环境
- WSDBIT 工具 WDK 中，网络拓扑
- WSDAPI 基本互操作性工具 WDK、 网络拓扑
- WDK WSDBIT 的测试环境
- WSDBIT 工具 WDK，服务
- WSDAPI 基本互操作性工具 WDK 服务
- SimpleService 服务 WDK WSDBIT
- AttachmentService 服务 WDK WSDBIT
- EventingService 服务 WDK WSDBIT
- WSDBIT 工具 WDK，设备以进行测试
- WSDAPI 基本互操作性工具 WDK，设备以进行测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12ab3579852663f75f141ad19844df19ce5994fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373152"
---
# <a name="wsdbit-testing-environment"></a>WSDBIT 测试环境


本主题介绍的物理环境和设备和其托管的服务功能。

### <a name="span-idnetworkmodelspanspan-idnetworkmodelspannetwork-model"></a><span id="network_model"></span><span id="NETWORK_MODEL"></span>网络模型

设备和客户端来测试已连接到以太网网络段，并构成单个的 IP 子网。 （例如 IPv4、 IPv6 或主机名） 的网络寻址方案不相关只要客户端和设备的共同支持至少一个方案必须只有一个设备和子网上的一个客户端。

为了便于调试和故障排除，应使用网络监视器来监视设备和客户端之间的流量交换。 若要监视的所有流量，必须通过以太网集线器的网络段连接的设备和客户端。 未提供一个中心时您可能能够通过运行 WSDBIT 的计算机上安装网络监视器监视流量。

下图显示了包含设备、 客户端和网络监视器 — 所有通过集线器连接的网络拓扑。

![说明 wsdapi 基本互操作性工具 (wsdbit) 进行测试的网络拓扑关系图](images/wsdbit1.png)

### <a name="span-idtestdevicespanspan-idtestdevicespantest-device"></a><span id="test_device"></span><span id="TEST_DEVICE"></span>测试设备

若要参与的设备端测试，应遵循以下通用原则中所述实现设备。 有关设备实现的详细信息，请参阅[WSDBIT 引用](wsdbit-reference.md)并[设备配置文件的 Web 服务 (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=163864)规范。

下表描述了服务和互操作性测试用例依赖项。

方案 SimpleService AttachmentService EventingService 设备和服务检查

一个或多个 SimpleService、 AttachmentService 或 EventingService

设备控制

X

附件

X

事件处理

X

 

测试设备应承载三种类型的服务：

-   http://schemas.example.org/SimpleService

-   http://schemas.example.org/AttachmentService

-   http://schemas.example.org/EventingService

### <a name="span-idsimpleservicespanspan-idsimpleservicespansimpleservice"></a><span id="simpleservice"></span><span id="SIMPLESERVICE"></span>SimpleService

**SimpleService**服务有四个方法：

-   **OneWay**是具有一个整数作为参数的单向方法。

-   **TwoWay**是具有两个整数在请求和响应中这些整数之和的请求-响应方法。

-   **一次**是具有许多不同类型的请求中和在响应中，包括一个布尔值，decimal、 float 和 Url 列表相同的类型的请求-响应方法。

-   **AnyCheck**响应中返回具有在请求中的 XML 片段和相同的段的请求-响应方法。

### <a name="span-idattachmentservicespanspan-idattachmentservicespanattachmentservice"></a><span id="attachmentservice"></span><span id="ATTACHMENTSERVICE"></span>AttachmentService

**AttachmentService**服务发送和接收附件。 若要发送和接收的附件数据包含在\\互操作目录作为两个单独的文件：Image1.jpg 和 Image2.jpg。 此服务具有两种方法：

-   **OneWayAttachment**是具有作为参数的附件的单向方法。

-   **TwoWayAttachment**是带附件的请求和响应的请求-响应方法。

### <a name="span-ideventingservicespanspan-ideventingservicespaneventingservice"></a><span id="eventingservice"></span><span id="EVENTINGSERVICE"></span>EventingService

**EventingService**服务有两种可以订阅事件：

-   **SimpleEvent**是不带参数的事件。

-   **IntegerEvent**是一个事件，返回一个整数。

### <a name="span-idimplementingtestservicesspanspan-idimplementingtestservicesspanimplementing-test-services"></a><span id="implementing_test_services"></span><span id="IMPLEMENTING_TEST_SERVICES"></span>实现测试服务

若要进行所有互操作性测试用例，您必须实现所有这些服务。 在这种情况下，在首次启动后设备承载每个服务的一个的实例。

但是，如果你想要实现仅其中一些服务，请参阅有关服务和互操作测试用例依赖关系信息本主题开头的表。

**请注意**  尝试任何高级互操作性方案 (如[设备控制](device-control-scenarios.md)，[附件](attachments-scenarios.md)，并[事件处理](eventing-scenarios.md))，则测试设备必须至少支持[设备和服务检查测试用例](device-and-service-inspection-scenarios.md)。 如果设备无法此测试用例，您可能无法继续使用高级测试用例。

 

测试设备和 WSDBIT 设备 (WSDBIT\_服务器) 必须能够执行以下操作：

-   显示的整数输入的参数**SimpleService**单向方法。

-   显示双向类型检查请求中提交的类型的值。

-   验证的已知的附件，应有和必须显示此验证的结果根据接收的附件。

-   启动每个两种类型的事件中所述**EventingService**通过手动输入或计时器。

-   显示在可扩展中收到的数据 (**xs： 任何**) 部分。

-   使用**xs: anyuri testdevice**作为**wsd:Scopes**发现的元素。

 

 





