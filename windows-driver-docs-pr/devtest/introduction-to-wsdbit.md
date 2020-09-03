---
title: WSDBIT 简介
description: WSDBIT 简介
ms.assetid: 8a8ee9de-95b2-43df-ba96-3b09fcd5751c
keywords:
- WSDBIT 工具 WDK，关于
- WSDAPI 基本互操作性工具 WDK，关于
- 适用于设备的 Web 服务 API WDK，关于
- WSDAPI WDK，关于
- 互操作性测试 WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a00ae63c8b3424281abbda2df773dbe131e06191
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384557"
---
# <a name="introduction-to-wsdbit"></a>WSDBIT 简介


用于设备的 Web 服务 (WSD) API (WSDAPI) 启用以下类型的消息交换：

-   发现 DPWS 设备。

-   描述 DPWS 设备。 这称为 *元数据交换*。

-   向 DPWS 服务发送服务特定消息以及二进制附件。

-   订阅和接收来自 DPWS 服务的事件。

如下图所示，WSDAPI 基本互操作性工具 (WSDBIT) 使用 WSDAPI 来发送和接收 DPWS 消息。 WSDBIT 可用于测试客户端中运行的 WSDAPI 与设备中运行的 DPWS 堆栈之间的互操作性。

![阐释 wsdapi 基本互操作性工具的示意图 (wsdbit) 和相关组件](images/wsdbit2.png)

[互操作性方案](client-scenarios-for-wsdbit.md)旨在验证消息格式以及前面的消息交换中使用的协议。 方案是从客户端角度定义的，并分为以下几类：

-   *设备和服务检查* 测试并验证 DPWS 设备发现和元数据交换。

-   *简单和高级控制* 测试并验证服务特定消息。

-   根据[SOAP 消息传输优化机制](https://www.w3.org/TR/2005/REC-soap12-mtom-20050125/)中的定义，*附件*测试和验证消息附件 (MTOM) 规范。

-   *事件* 测试并验证 [Web 服务事件](/previous-versions/ms951233(v=msdn.10))。

-   *安全通信* 包括上述所有方案中的元素。

根据互操作性测试的具体需要，可以实现设备和/或客户端。

你还可以有选择地实现测试用例的各个部分。 例如，你只能实现 [设备和服务检查](device-and-service-inspection-scenarios.md) 以及 [简单和高级控制](device-control-scenarios.md) 互操作性测试事例。

**注意**   你至少必须实现设备和服务检查互操作性测试事例，因为其他测试用例需要该测试用例。

 

 

