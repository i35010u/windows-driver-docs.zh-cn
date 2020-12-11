---
title: 硬件通知支持
description: Windows 10 版本 1709 的基础结构可以为 LED 和振动机制等通知组件提供不区分硬件的支持。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da620d817b7bcd8de577d39b6325d479744b2e81
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091130"
---
# <a name="hardware-notifications-support"></a>硬件通知支持


**适用于**

-   驱动程序开发人员和 Oem

**重要的 API**

Windows 10 版本 1709 的基础结构可以为 LED 和振动机制等通知组件提供不区分硬件的支持。 实现此支持的方式是引入内核模式驱动程序框架 (KMDF) 类扩展，该扩展专用于硬件通知组件，因此可以快速开发客户端驱动程序。 KMDF 类扩展实质上是 KMDF 驱动程序，它为给定的设备类提供一组定义的功能，类似于 Windows 驱动程序模型 (WDM) 中的端口驱动程序。 此部分概述硬件通知类扩展的体系结构。 有关 KMDF 的其他信息，请参阅 [Using WDF to Develop a Driver](../wdf/using-the-framework-to-develop-a-driver.md)（使用 WDF 来开发驱动程序）。

## <a name="span-idhardware_notification_class_extensionspanspan-idhardware_notification_class_extensionspanspan-idhardware_notification_class_extensionspanhardware-notification-class-extension"></a><span id="Hardware_notification_class_extension"></span><span id="hardware_notification_class_extension"></span><span id="HARDWARE_NOTIFICATION_CLASS_EXTENSION"></span>硬件通知类扩展


硬件通知类扩展是硬件通知驱动程序体系结构的核心组件。 类扩展旨在最大程度地减少与 KMDF 的必要交互，而是提供一个简单界面来控制通知组件。 类扩展处理如下任务：

-   客户端驱动程序的注册
-   系统资源的分配和清理
-   注册客户端驱动程序的 PnP 电源回调函数
-   为客户端驱动程序注册 i/o 队列
-   数据验证和错误检查
-   向客户端驱动程序通信硬件请求

下图说明了基本的硬件通知类扩展体系结构。

![hwn clx 体系结构](images/oem-hwnclx-arch.png)

## <a name="span-idhardware_notification_client_driverspanspan-idhardware_notification_client_driverspanspan-idhardware_notification_client_driverspanhardware-notification-client-driver"></a><span id="Hardware_notification_client_driver"></span><span id="hardware_notification_client_driver"></span><span id="HARDWARE_NOTIFICATION_CLIENT_DRIVER"></span>硬件通知客户端驱动程序


通过使用硬件通知类扩展，可以轻松地为硬件通知组件生成客户端驱动程序。 客户端驱动程序的唯一职责是为 KMDF 提供适当的入口点，实现定义的类扩展回叫函数，管理电源状态，并控制物理硬件。 具体而言，客户端驱动程序必须实现 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 和 [*.Evt \_ WDF \_ 驱动程序 \_ 设备 \_ 添加*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数以供 Windows driver Foundation (WDF) ，以及类扩展所需的回调函数。

下图说明了客户端驱动程序的透视的交互。

![客户端驱动程序](images/oem-hwnclx-clientarch.png)

 

