---
title: 硬件通知支持
description: Windows 10 版本1709为通知组件（例如 Led 和振动机制）的硬件不可知支持提供基础结构。
ms.assetid: 48df55c4-aa5e-4157-8b90-65ad127d876b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f340e2d97cc6bff117d5908158c4ba239e4d3724
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824897"
---
# <a name="hardware-notifications-support"></a>硬件通知支持


**适用于**

-   驱动程序开发人员和 Oem

**重要的 API**

-   [硬件通知参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

Windows 10 版本1709为通知组件（例如 Led 和振动机制）的硬件不可知支持提供基础结构。 实现此支持的方式是引入内核模式驱动程序框架 (KMDF) 类扩展，该扩展专用于硬件通知组件，因此可以快速开发客户端驱动程序。 KMDF 类扩展实质上是 KMDF 驱动程序，它为给定的设备类提供一组定义的功能，类似于 Windows 驱动程序模型 (WDM) 中的端口驱动程序。 此部分概述硬件通知类扩展的体系结构。 有关 KMDF 的其他信息，请参阅 [Using WDF to Develop a Driver](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)（使用 WDF 来开发驱动程序）。

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


通过使用硬件通知类扩展，可以轻松地为硬件通知组件生成客户端驱动程序。 客户端驱动程序的唯一职责是为 KMDF 提供适当的入口点，实现定义的类扩展回叫函数，管理电源状态，并控制物理硬件。 具体而言，客户端驱动程序必须实现[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)和[ *.evt\_WDF\_驱动程序\_设备\_添加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数以供 WINDOWS driver Foundation （WDF）使用，以及所需的回调类扩展的函数。

下图说明了客户端驱动程序的透视的交互。

![客户端驱动程序](images/oem-hwnclx-clientarch.png)

 

 




