---
title: WSDBIT 简介
description: WSDBIT 简介
ms.assetid: 8a8ee9de-95b2-43df-ba96-3b09fcd5751c
keywords:
- WSDBIT 工具有关 WDK，
- WSDAPI 基本互操作性工具有关 WDK，
- 有关 web 服务的设备 API WDK
- WSDAPI WDK，关于
- 互操作性测试 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad97975e0ead86529c1b5891ea8ad691f3d9b63d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356554"
---
# <a name="introduction-to-wsdbit"></a>WSDBIT 简介


Web 服务的 Devices (WSD) API (WSDAPI)，以下类型的消息交换：

-   发现 DPWS 设备。

-   描述 DPWS 设备。 这被称为*元数据交换*。

-   将特定于服务的消息，以及二进制附件，发送往和来自 DPWS 服务。

-   订阅并从 DPWS 服务接收事件。

下图中所示，WSDAPI 基本互操作性工具 (WSDBIT) 使用 WSDAPI 发送和接收 DPWS 消息。 WSDBIT 可以用于测试 WSDAPI 中运行客户端，在设备中运行的 DPWS 堆栈之间的互操作性。

![说明 wsdapi 基本互操作性工具 (wsdbit) 和相关的组件的关系图](images/wsdbit2.png)

[互操作性方案](client-scenarios-for-wsdbit.md)旨在验证以及在前面的消息交换中使用的协议消息格式。 从客户端透视定义的方案和分为以下类别：

-   *设备和服务检查*测试和验证 DPWS 设备发现和元数据交换。

-   *简单和高级控制*测试和验证特定于服务的消息。

-   *附件*测试和验证邮件附件中定义[SOAP 消息传输优化机制 (MTOM)](https://go.microsoft.com/fwlink/p/?linkid=81254)规范。

-   *Eventing*测试和验证[Web 服务事件](https://go.microsoft.com/fwlink/p/?linkid=81245)。

-   *保护通信*包括所有上述方案的元素。

根据互操作性测试的特定需求，可以实现，客户端，和 / 或设备。

您可以有选择地实现测试用例的部分。 例如，可以仅实现[设备和服务检查](device-and-service-inspection-scenarios.md)并[简单和高级控制](device-control-scenarios.md)互操作性测试用例。

**请注意**  至少，您必须实现设备和服务检查互操作性测试用例，因为其他测试用例需要它。

 

 

 





