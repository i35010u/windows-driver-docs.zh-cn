---
title: 传感器驱动程序的体系结构概述
description: '传感器设备驱动程序是通过使用 Windows 用户模式驱动程序框架（ (UMDF）实现的 COM 对象) '
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: efe69e7de250527b77df35c45b179344b3112794
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831077"
---
# <a name="architecture-overview-for-sensor-drivers"></a>传感器驱动程序的体系结构概述


传感器设备驱动程序是通过使用 Windows 用户模式驱动程序框架 (UMDF) 实现的 COM 对象。 传感器驱动程序将 (WPD) 接口和其他类型的 Windows 便携式设备用作帮助程序对象。 Windows 驱动程序工具包文档中记录了 UMDF 和 WPD。 有关 UMDF 驱动程序的详细信息，请参阅 [用户模式驱动程序框架](../wdf/user-mode-driver-framework-design-guide.md)。 有关 WPD 类型的详细信息，请参阅 [便携设备](/previous-versions/windows/hardware/drivers/ff597901(v=vs.85))。

传感器驱动程序使用特殊的 **类扩展** 对象。 传感器类扩展是标准 COM 对象，它提供了一个标准的实现来处理传感器设备驱动程序的 i/o 请求。 传感器驱动程序会在驱动程序的进程中创建类扩展对象，然后使用设备驱动程序接口 (DDI) 将 i/o 请求转发到和从类扩展接收事件。 下图显示传感器、其驱动程序和传感器类扩展之间的关系。  (传感器驱动程序为每个传感器设备创建类扩展的新实例。 ) 

![使用传感器类扩展的基于 umdf 的传感器驱动程序](images/sensordriver-cxt.jpg)

有关类扩展对象的详细信息，请参阅 [关于传感器类扩展](about-the-sensor-class-extension.md)。

>[!IMPORTANT]
> 传感器驱动程序必须是自由线程的并且是线程安全的。
