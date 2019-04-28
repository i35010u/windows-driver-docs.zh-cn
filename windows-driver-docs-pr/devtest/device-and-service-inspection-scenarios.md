---
title: 设备和服务检查方案
description: 设备和服务检查方案
ms.assetid: 25e6ed92-e01c-4349-a614-b71bb08d71cd
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
- 设备和服务检查方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6870686ffc84ece4e16b5dc6b522defddff198
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329689"
---
# <a name="device-and-service-inspection-scenarios"></a>设备和服务检查方案


设备和服务检查方案测试设备发现和后续的设备和服务检查。

基本发现的设备和托管的服务方案的其余部分提供的基础结构。

设备必须使用**xs: anyuri testdevice**作为**wsd:Scopes**发现的元素。

下表描述了此方案。

单步客户端操作服务器操作启用通过/失败条件**1.1**

**TestDevice 启动\\关闭**

1.1.1

无

TestDevice 启动，并将发送 Hello。

在客户端正确接收 hello。

1.1.2

无

TestDevice 关闭，并将发送 Bye。

在客户端正确接收 bye。 **Wsa: endpointreference / wsa： 地址**应与在步骤 1.1.1 中使用的一个相同。

1.1.3

无

TestDevice 重新启动，并将发送 Hello。

正确收到具有相同的元数据版本在 1.1.1 hello。 **Wsa: endpointreference / wsa： 地址**应与在步骤 1.1.1 中使用的一个相同。

**1.2**

**解决的 TestDevice**

1.2.1

发送解析。

使用 ResolveMatches 做出响应。

转到步骤 1.2.2。

1.2.2

发送到 TestDevice GetMetadaRequest。

使用 GetMetadatResponse 做出响应。

转到步骤 1.2.3。

1.2.3

显示 ThisDevice 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.2.4

显示 ThisModel 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.2.5

显示主机，托管服务，EndpointReference。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.2.6

发送的 urn: uuid:00000000 解析-0000-0000-0000-000000000000 (即 i **wsa: endpointreference / wsa： 地址**的设备)。

无。 因为设备不符合这**wsa: endpointreference / wsa： 地址**，它不应响应

服务器不响应任何 ResolveMatches 消息。

**1.3**

**TestDevice 探测**

1.3.1

发送探测的通配符：

-   使用默认的匹配规则。

-   否**wsd:Types**元素。

-   否**wsd:Scopes**元素。

使用 ProbeMatches 做出响应。

转到步骤 1.3.2 （或 1.3.3）。

1.3.2 （可选。 此步骤是必需的仅当没有**wsd:XAddrs**中 1.3.1 ProbeMatches 中提供。)

发送到解决**wsa: endpointreference / wsa:Addres**s 从 1.2.1 ProbeMatches 中指定。

使用 ResolveMatches 做出响应。

转到步骤 1.3.3。

1.3.3

发送到 TestDevice GetMetadataRequest。

使用 GetMetadataResponse 做出响应。

转到步骤 1.3.4。

1.3.4

显示 ThisDevice 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.3.5

显示 ThisModel 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.3.6

显示主机，托管服务，EndpointReference。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.3.7

发送的探测，指定以下：

-   使用默认的匹配规则。

-   要匹配类型： **wsdp:Device**。 (.请参阅命名空间表更高版本，以及设备配置文件中的 R1020 Web 服务。）

-   没有 wsd:Scopes 的元素。

使用 ProbeMatches 做出响应。

值**wsa: endpointreference / wsa： 地址**与在步骤 1.2.1 时相同。

1.3.8

发送的探测，指定以下：

-   在中定义的匹配规则，它是使用[Web 服务动态发现 (Ws-discovery)](https://go.microsoft.com/fwlink/p/?linkid=81240)规范。

-   没有 wsd:Types 的元素。

-   使用以下代码作为作用域*testdevice*。

使用 ProbeMatches 做出响应。

值**wsa: endpointreference / wsa： 地址**与在步骤 1.2.1 时相同。

1.3.9

发送的探测，指定以下：

-   使用[Web 服务的设备配置文件](https://go.microsoft.com/fwlink/p/?linkid=163864)匹配规则。

-   否**wsd:Types**元素。

-   使用以下代码作为作用域*testDEVICE*。

无。 此测试不会响应 ProbeMatches。

接收不到任何消息;等待 10 秒。

1.3.10

发送的探测，指定以下：

-   使用默认的匹配规则。

-   使用虚构的类型进行匹配: (例如， http://example.org/this/wont/work:Device)。

-   否**wsd:Scopes**元素。

无。 此测试不会响应 ProbeMatches。

接收不到任何消息;等待 10 秒。

**1.4**

**定向的探测**

1.4.1

作为 HTTP 请求发送探测的通配符：

-   使用默认的匹配规则。

-   否**wsd:Types**元素。

-   否**wsd:Scopes**元素。

-   提供的 HTTP 地址。

通过使用 HTTP 响应 ProbeMatches 做出响应。

确认**wsa: endpointreference / wsa： 地址**TestDevice 是正确。

**1.5**

**获取元数据，而无需发现**

1.5.1

发送到 TestDevice GetMetadataRequest。

使用 GetMetadataResponse 做出响应。

转到步骤 1.5.2。

1.5.2

显示 ThisDevice 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.5.3

显示 ThisModel 元数据。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.5.4

显示主机，托管服务，EndpointReference。

无

对应于已发送的内容。 客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

 

 

 





