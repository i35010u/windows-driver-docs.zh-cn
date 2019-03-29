---
title: 传感器驱动程序的体系结构概述
description: 传感器设备驱动程序都是通过使用 Windows 用户模式驱动程序框架 (UMDF) 实现的 COM 对象
ms.assetid: 6d1b15ea-ba27-4bde-8000-d31f014ab47d
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3617232bcb436851c4302320f2c41a5edd5e50b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577064"
---
# <a name="architecture-overview-for-sensor-drivers"></a>传感器驱动程序的体系结构概述


传感器设备驱动程序是通过使用 Windows 用户模式驱动程序框架 (UMDF) 实现的 COM 对象。 传感器驱动程序使用 Windows 便携式设备 (WPD) 接口和其他类型作为帮助程序对象。 Windows 驱动程序工具包文档中说明了 UMDF 和 WPD。 有关 UMDF 驱动程序的详细信息，请参阅[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff561365)。 有关 WPD 类型的详细信息，请参阅[便携设备](https://msdn.microsoft.com/library/windows/hardware/ff597901)。

传感器驱动程序将使用一个特殊**类扩展**对象。 传感器类扩展标准的 COM 对象，提供了用于处理传感器设备驱动程序的 I/O 请求的标准实现。 传感器驱动程序在驱动程序的过程中创建的类扩展对象，然后使用设备驱动程序接口 (DDI) 以转发到的 I/O 请求和接收来自此类扩展的事件。 下图显示了一个传感器、 驱动程序、 与传感器类扩展之间的关系。 （传感器驱动程序创建适用于每个传感器设备的类扩展的新实例。）

![使用传感器类扩展的 umdf 基于传感器驱动程序](images/sensordriver-cxt.jpg)

有关类扩展对象的详细信息，请参阅[有关传感器类扩展](about-the-sensor-class-extension.md)。

>[!IMPORTANT]
> 传感器驱动程序必须自由线程和线程安全。










