---
title: 驱动程序 I/O 模型
description: 通过简单的外围总线、 系统 GPIO 插针和资源中心进行通信的示例驱动程序和加速感应器。
ms.assetid: 69368837-0599-497F-883C-608DFE014C7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e8e2498ca01c37a773782b4b74af4f3ca554cfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525080"
---
# <a name="the-driver-io-model"></a>驱动程序 I/O 模型


通过简单的外围总线、 系统 GPIO 插针和资源中心进行通信的示例驱动程序和加速感应器。

下图描绘了在组织运行的组件： 用户模式和内核模式下，实际的硬件。

![io 关系图](images/io.png)

## <a name="simple-peripheral-bus-spb"></a>简单的外围总线 （存储）


Windows 8.1 支持简化了开发和实现存储控制器驱动程序的类扩展的窗体中的存储组件。 一般情况下，该组件提供如下功能：

-   资源中心包括注册和设置检索处理所有通信。
-   实现分层的队列结构来管理同步目标和总线锁定请求
-   将转换到内核模式从用户模式缓冲区

## <a name="general-purpose-inputoutput-gpio"></a>常规用途输入/输出 (GPIO)


Windows 8.1 支持驻留在同一级别作为内核模式存储组件的 GPIO 类扩展。 同时提供驱动程序的客户端的标准接口，GPIO 类扩展可用于在基础硬件连接和 GPIO 位置的灵活性。

在 SoC 平台 GPIO 插针是分散到芯片，以及其他组件，如 SPI 连接调制解调器上公开。

## <a name="resource-hub"></a>资源中心


Windows 8.1 支持用于管理所有设备和总线控制器间的连接资源中心。 所需的启动和停止排序的中心保证进行维护。

中心是专门针对 SoC 平台和其平面设备树的组件。 在这些系统上的总线不同从电脑中通过以下方式：

-   连接是通常无法发现的;它们在 ACPI 以静态方式定义
-   硬件组件通常具有跨越多个总线，而不是严格的父-子关系的多个依赖项

## <a name="related-topics"></a>相关主题
[SpbAccelerometer 驱动程序示例](spbaccelerometer-driver-sample.md)  
[使用传感器类扩展](using-the-sensor-class-extension.md)  



