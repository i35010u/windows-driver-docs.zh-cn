---
title: WSDBIT 的客户端方案
description: WSDBIT 的客户端方案
ms.assetid: fb692c83-b384-492d-84fb-10e00db9f30f
keywords:
- WSDBIT 工具 WDK，测试方案
- WSDAPI 基本互操作性工具 WDK，测试方案
- 方案 WDK WSDBIT
- 测试方案 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 255650478e72e6a4342f27307f555d685acc8d0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343971"
---
# <a name="client-scenarios-for-wsdbit"></a>WSDBIT 的客户端方案


所有测试方案是由于从客户端的角度来看。 在有限情况下，设备交互都需要为完成的方案。 此要求的各自方案所示。

除非另行说明，假定测试设备 (TestDevice) 已启动并且可在其运行这些方案的网络段上。

某些情况下在 TestDevice 中定义客户端和一个 （或以上） 的托管服务之间的交互。

客户端可以获取托管服务中的终结点有两种

-   可由用户提供托管服务终结点。 这种情况意味着，在此之后 TestDevice 已开始，将终结点已知与可对已知的参与方的正在运行客户端。

-   可以动态发现托管服务终结点。 这种情况意味着发现 TestDevice。 发现 TestDevice 可能通过：

    -   Hello (假定它从设备启动以及是否有**XAddrs**字段)。
    -   探测\\解决 exchange。
    -   解决消息 (其中假定*urn: uuid*已知设备终结点地址)。

    然后可以请求元数据和托管服务元数据的后续检查将显示终结点。

客户端可以选择以支持其中一种方法，但 TestDevice 必须支持这两种方法来获取托管服务终结点。

客户端必须能够验证 TestDevice 从收到的附件。 应通过加载到内存中预期的附件的副本并执行操作上收到的附件的字节的字节的内存比较验证附件。

当客户端发送的事件的续订时，他们可以选择手动启动续订或自动将续订发送时的原始 SubscribeResponse 消息中指定的续订期间下半部分已过。

**请注意**  因为测试用例可能依赖于以前的测试用例的结果，应按顺序运行测试用例。 （例如，1.3.8 取决于 1.2.1 的结果。）测试 （例如，事件和附件方案中） 之间的方案之间有任何依赖关系。 无法发现 TestDevice 并检查其托管的服务将阻止特定的高级的方案执行在于在第一个方案 （设备和服务检测） 的所有高级方案的隐式依赖关系。

 

本部分包括以下主题：

[设备和服务检查方案](device-and-service-inspection-scenarios.md)

[设备管理方案](device-control-scenarios.md)

[附件方案](attachments-scenarios.md)

[事件处理方案](eventing-scenarios.md)

[安全通信方案](secure-communication-scenarios.md)

 

 





