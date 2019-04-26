---
title: 硬件通知支持
description: Windows 10 版本 1709年通知组件，如 Led 和振动机制的硬件不可知支持提供了基础结构。
ms.assetid: 48df55c4-aa5e-4157-8b90-65ad127d876b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2bacf4a97294dbf5a5888dd33f337edb0ae7e624
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326102"
---
# <a name="hardware-notifications-support"></a>硬件通知支持


**适用于**

-   驱动程序开发人员和 Oem

**重要的 Api**

-   [硬件通知参考](https://msdn.microsoft.com/library/windows/hardware/dn789336)

Windows 10 版本 1709年通知组件，如 Led 和振动机制的硬件不可知支持提供了基础结构。 实现此支持的方式是引入内核模式驱动程序框架 (KMDF) 类扩展，该扩展专用于硬件通知组件，因此可以快速开发客户端驱动程序。 KMDF 类扩展实质上是 KMDF 驱动程序，它为给定的设备类提供一组定义的功能，类似于 Windows 驱动程序模型 (WDM) 中的端口驱动程序。 此部分概述硬件通知类扩展的体系结构。 有关 KMDF 的其他信息，请参阅 [Using WDF to Develop a Driver](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)（使用 WDF 来开发驱动程序）。

## <a name="span-idhardwarenotificationclassextensionspanspan-idhardwarenotificationclassextensionspanspan-idhardwarenotificationclassextensionspanhardware-notification-class-extension"></a><span id="Hardware_notification_class_extension"></span><span id="hardware_notification_class_extension"></span><span id="HARDWARE_NOTIFICATION_CLASS_EXTENSION"></span>硬件通知类扩展


硬件通知类扩展是硬件通知驱动程序体系结构的主要组件。 类扩展旨在最大程度减少与 KMDF 的必要交互并改为通知组件的控件提供一个简单的接口。 类扩展处理的任务如：

-   客户端驱动程序的注册
-   分配和系统资源清理
-   客户端驱动程序的即插即用 power 回调函数的注册
-   I/O 队列用于客户端驱动程序的注册
-   数据验证和错误检查
-   硬件对的请求的客户端驱动程序的通信

下图演示了基本硬件通知类扩展体系结构。

![hwn clx 体系结构](images/oem-hwnclx-arch.png)

## <a name="span-idhardwarenotificationclientdriverspanspan-idhardwarenotificationclientdriverspanspan-idhardwarenotificationclientdriverspanhardware-notification-client-driver"></a><span id="Hardware_notification_client_driver"></span><span id="hardware_notification_client_driver"></span><span id="HARDWARE_NOTIFICATION_CLIENT_DRIVER"></span>硬件通知客户端驱动程序


客户端驱动程序可以轻松地生成硬件通知组件通过硬件通知类扩展。 客户端驱动程序的唯一职责是提供相应的入口点对于 KMDF、 实现定义的类扩展回调函数、 管理电源状态和控制的物理硬件。 具体而言，客户端驱动程序必须实现[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)并[ *EVT\_WDF\_驱动程序\_设备\_添加*](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数以用于通过 Windows Driver Foundation (WDF)，以及此类扩展的必需的回调函数。

下图说明了从客户端驱动程序的角度来看的交互。

![客户端驱动程序体系结构](images/oem-hwnclx-clientarch.png)

 

 




