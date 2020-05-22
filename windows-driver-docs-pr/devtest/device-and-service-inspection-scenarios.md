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
ms.openlocfilehash: 03e99fa225a7d6784529272b413b81f406c5558c
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769627"
---
# <a name="device-and-service-inspection-scenarios"></a>设备和服务检查方案


设备和服务检查方案将测试设备发现以及后续的设备和服务检查。

设备和托管服务的基本发现为其余方案提供基础结构。

设备必须使用**xs： anyURI testdevice**作为**wsd： scope**元素才能发现。

下表描述了这种情况。

步骤客户端操作服务器操作通过-失败条件**1.1**

**TestDevice 启动 \\ 关闭**

1.1.1

Nothing

TestDevice 启动并发送 Hello。

已在客户端正确接收 Hello。

1.1.2

Nothing

TestDevice 关闭并发送再见。

在客户端正确接收了再见。 **Wsa： EndpointReference/wsa： Address**应与步骤1.1.1 中使用的地址相同。

1.1.3

Nothing

TestDevice 重新启动并发送 Hello。

已在1.1.1 中正确接收到与相同的元数据版本。 **Wsa： EndpointReference/wsa： Address**应与步骤1.1.1 中使用的地址相同。

**1.2**

**解析 TestDevice**

1.2.1

发送解析。

使用 ResolveMatches 响应。

请参阅步骤1.2.2。

1.2.2

将 GetMetadaRequest 发送到 TestDevice。

使用 GetMetadatResponse 响应。

请参阅步骤1.2.3。

1.2.3

显示 ThisDevice 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.2.4

显示 ThisModel 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.2.5

显示主机，HostedService，EndpointReference。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.2.6

为 urn 发送解析： uuid：00000000-0000-0000-0000-000000000000 （这是设备的**wsa： EndpointReference/wsa： Address** ）。

无。 因为设备不匹配此**wsa： EndpointReference/wsa： Address**，所以它不应响应

服务器不响应任何 ResolveMatches 消息。

**1.3**

**探测 TestDevice**

1.3.1

发送通配符探测：

-   使用默认匹配规则。

-   无**wsd： Types**元素。

-   无**wsd：范围**元素。

使用 ProbeMatches 响应。

请参阅步骤1.3.2 （或1.3.3）。

1.3.2 （可选。 只有在1.3.1 的 ProbeMatches 中未提供**wsd： XAddrs**的情况下，才需要执行此步骤。）

将解析发送到在 ProbeMatches from 1.2.1 中指定的**wsa： EndpointReference/wsa：邮件**。

使用 ResolveMatches 响应。

请参阅步骤1.3.3。

1.3.3

将 GetMetadataRequest 发送到 TestDevice。

使用 GetMetadataResponse 响应。

请参阅步骤1.3.4。

1.3.4

显示 ThisDevice 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.3.5

显示 ThisModel 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.3.6

显示主机，HostedService，EndpointReference。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.3.7

发送指定以下内容的探测：

-   使用默认匹配规则。

-   要匹配的类型： **wsdp： Device**。 (.请参阅上面的命名空间表以及 Web Services 的设备配置文件中的 R1020。）

-   无 wsd：范围元素。

使用 ProbeMatches 响应。

**Wsa： EndpointReference/wsa： Address**的值与步骤1.2.1 中的值相同。

1.3.8

发送指定以下内容的探测：

-   使用在[Web Services 动态发现（WS 发现）](http://schemas.xmlsoap.org/ws/2005/04/discovery/)规范中定义的匹配规则。

-   无 wsd： Types 元素。

-   使用以下作为范围*testdevice*。

使用 ProbeMatches 响应。

**Wsa： EndpointReference/wsa： Address**的值与步骤1.2.1 中的值相同。

1.3.9

发送指定以下内容的探测：

-   使用 "[设备配置文件" 作为 "Web 服务](http://schemas.xmlsoap.org/ws/2006/02/devprof/)匹配规则"。

-   无**wsd： Types**元素。

-   使用以下作为范围*testDEVICE*。

无。 此测试不响应 ProbeMatches。

未收到任何消息;等待10秒。

1.3.10

发送指定以下内容的探测：

-   使用默认匹配规则。

-   使用要匹配的虚构类型：（例如， http://example.org/this/wont/work:Device) 。

-   无**wsd：范围**元素。

无。 此测试不响应 ProbeMatches。

未收到任何消息;等待10秒。

**1.4**

**定向探测**

1.4.1

发送通配符探测作为 HTTP 请求：

-   使用默认匹配规则。

-   无**wsd： Types**元素。

-   无**wsd：范围**元素。

-   提供 HTTP 地址。

使用 HTTP 响应的 ProbeMatches 响应。

确认 TestDevice 的**wsa： EndpointReference/wsa： Address**正确。

**1.5**

**未发现的情况下获取元数据**

1.5.1

将 GetMetadataRequest 发送到 TestDevice。

使用 GetMetadataResponse 响应。

请参阅步骤1.5.2。

1.5.2

显示 ThisDevice 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.5.3

显示 ThisModel 元数据。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

1.5.4

显示主机，HostedService，EndpointReference。

Nothing

对应于发送的内容。 有关客户端输出的示例，请参阅[示例元数据响应输出](sample-metadata-response-output.md)。

 

 

 





