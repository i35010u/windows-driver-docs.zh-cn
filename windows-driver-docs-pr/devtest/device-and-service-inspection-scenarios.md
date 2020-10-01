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
ms.openlocfilehash: 02e685dc111358d47a0fb7d2229ca9b8438a5211
ms.sourcegitcommit: cccf9ba62af357aad1016addbbf6c42c7f564412
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2020
ms.locfileid: "91606475"
---
# <a name="device-and-service-inspection-scenarios"></a>设备和服务检查方案

设备和服务检查方案将测试设备发现以及后续的设备和服务检查。

设备和托管服务的基本发现为其余方案提供基础结构。

设备必须使用 **xs： anyURI testdevice** 作为 **wsd： scope** 元素才能发现。

下表描述了这种情况。

|步骤|客户端操作|服务器操作|通过失败的条件|
|----|----|----|----|
|**1.1**|**TestDevice 启动 \\ 关闭**| | |
|1.1.1|Nothing|TestDevice 启动并发送 Hello。|已在客户端正确接收 Hello。|
|1.1.2|Nothing|TestDevice 关闭并发送再见。|在客户端正确接收了再见。 **Wsa： EndpointReference/wsa： Address**应与步骤1.1.1 中使用的地址相同。|
|1.1.3|Nothing|TestDevice 重新启动并发送 Hello。|已在1.1.1 中正确接收到与相同的元数据版本。 **Wsa： EndpointReference/wsa： Address**应与步骤1.1.1 中使用的地址相同。|
|**1.2**|**解析 TestDevice**| | |
|1.2.1|发送解析。|使用 ResolveMatches 响应。|请参阅步骤1.2.2。|
|1.2.2|将 GetMetadaRequest 发送到 TestDevice。|使用 GetMetadatResponse 响应。|请参阅步骤1.2.3。|
|1.2.3|显示 ThisDevice 元数据。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.2.4|显示 ThisModel 元数据。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.2.5|显示主机，HostedService，EndpointReference。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.2.6|发送用于 urn： uuid： 00000000-0000-0000-0000-000000000000 (的解析，其位于) 设备的 **wsa： EndpointReference/wsa： Address** 。|哪个位置都不行。 因为设备不匹配此 **wsa： EndpointReference/wsa： Address**，所以它不会响应。|服务器不响应任何 ResolveMatches 消息。|
|**1.3**|**探测 TestDevice**| | |
|1.3.1|发送通配符探测：</br>-使用默认匹配规则。</br>-无 **wsd： Types** 元素。</br>-无 **wsd：范围** 元素。|使用 ProbeMatches 响应。|请参阅步骤 1.3.2 (或 1.3.3) 。|
|1.3.2 (可选。 只有在1.3.1 的 ProbeMatches 中未提供 **wsd： XAddrs** 的情况下，才需要执行此步骤。 ) |将解析发送到在 ProbeMatches from 1.2.1 中指定的 **wsa： EndpointReference/wsa：邮件**。|使用 ResolveMatches 响应。|请参阅步骤1.3.3。|
|1.3.3|将 GetMetadataRequest 发送到 TestDevice。|使用 GetMetadataResponse 响应。|请参阅步骤1.3.4。|
|1.3.4|显示 ThisDevice 元数据。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.3.5|显示 ThisModel 元数据。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.3.6|显示主机，HostedService，EndpointReference。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.3.7|发送指定以下内容的探测：</br>-使用默认匹配规则。</br>-要匹配的类型： **wsdp： Device**。  (。请参阅上面的命名空间表以及 Web Services 的设备配置文件中的 R1020。 ) </br>-无 wsd：范围元素。|使用 ProbeMatches 响应。|**Wsa： EndpointReference/wsa： Address**的值与步骤1.2.1 中的值相同。|
|1.3.8|发送指定以下内容的探测：</br>-使用在 [Web Services 动态发现 (ws-management) ](https://docs.oasis-open.org/ws-dd/discovery/1.1/os/wsdd-discovery-1.1-spec-os.html) 规范中定义的匹配规则。</br>-无 wsd： Types 元素。</br>-使用以下作为范围 *testdevice*。|使用 ProbeMatches 响应。|**Wsa： EndpointReference/wsa： Address**的值与步骤1.2.1 中的值相同。|
|1.3.9|发送指定以下内容的探测：</br>-将 [设备配置文件用于 Web 服务](https://docs.oasis-open.org/ws-dd/ns/dpws/2009/01) 匹配规则。</br>-无 **wsd： Types** 元素。</br>-使用以下作为范围 *testDEVICE*。|哪个位置都不行。 此测试不响应 ProbeMatches。|未收到任何消息;等待10秒。|
|1.3.10|发送指定以下内容的探测：</br>-使用默认匹配规则。</br>-使用要匹配的虚构类型，例如 `https://example.org/this/wont/work:Device` 。</br>-无 **wsd：范围** 元素。|哪个位置都不行。 此测试不响应 ProbeMatches。|未收到任何消息;等待10秒。|
|**1.4**|**定向探测**| | |
|1.4.1|发送通配符探测作为 HTTP 请求：</br>-使用默认匹配规则。</br>-无 **wsd： Types** 元素。</br>-无 **wsd：范围** 元素。</br>-提供了 HTTP 地址。|使用 HTTP 响应的 ProbeMatches 响应。|确认 TestDevice 的 **wsa： EndpointReference/wsa： Address** 正确。|
|**1.5**|**未发现的情况下获取元数据**| | |
|1.5.1|将 GetMetadataRequest 发送到 TestDevice。|使用 GetMetadataResponse 响应。|请参阅步骤1.5.2。|
|1.5.2|显示 ThisDevice 元数据。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.5.3|显示 ThisModel 元数据。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
|1.5.4|显示主机，HostedService，EndpointReference。|Nothing|对应于发送的内容。 有关客户端输出的示例，请参阅 [示例元数据响应输出](sample-metadata-response-output.md)。|
