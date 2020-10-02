---
title: 传感器设备驱动程序设计指南
description: 传感器设备驱动程序设计指南
ms.assetid: 74e8ae08-3e61-41be-aed0-e733dc6072cf
ms.date: 09/29/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: bfe90a660efcc7eb11824c304097eca2afb601e2
ms.sourcegitcommit: fc94eb0d5a41ef81c1b3ab91ad725386db0be0c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603701"
---
# <a name="introduction-to-the-sensor-and-location-platform-in-windows"></a>Windows 中的传感器和位置平台简介

Windows 操作系统为传感器设备提供本机支持。 此支持包括对位置传感器的支持，如 GPS 设备。 作为此支持的一部分，该平台为设备制造商提供了一种向软件开发人员和使用者呈现传感设备的标准方法。 同时，该平台向开发人员提供了一个用于处理传感器和传感器数据的标准化 API 和设备驱动程序接口 (DDI)。 本部分概要介绍 Windows 传感器和位置平台，讨论平台的各个部分，并介绍各部分如何协同工作，从而形成一个功能全面的传感器处理系统。

## <a name="sensor-device-overview"></a>传感设备概述

传感器的配置多种多样，从某种角度来说，几乎所有提供物理现象数据的装置都可以称为传感器。 虽然我们通常认为传感器是一种硬件设备，但逻辑传感器也可以通过在软件或固件中模拟传感器功能来提供信息。 此外，单个硬件设备可以包含多个传感器。

传感器和位置平台将传感器划分为不同的类别，这些类别是对传感器设备种类的宽泛划分，而类型则表示具体的传感器种类。 例如，视频游戏控制器中的传感器可探测玩家手的位置和运动（比如在视频保龄球游戏中），这类传感器将归为方向传感器，但其类型则是三维加速感应器。 在代码中，Windows 通过使用全局唯一标识符 (GUID) 来表示类别和类型，其中许多是预定义的。 设备制造商可以根据需要，通过定义并发布新的 GUID 来创建新的类别和类型。

位置设备是一种非常有趣的类别。 目前，大多数人都熟悉全球定位系统 (GPS)。 在 Windows 中，GPS 是“位置”类别中的一种传感器。 位置类别还可能包括其他传感器类型。 其中一些传感器类型是基于软件的，例如基于 Internet 地址提供位置信息的 IP 解析程序、根据附近的信号塔确定位置的移动手机信号塔三角仪，或通过 Wi-fi 网络确定位置的传感器。

## <a name="about-the-platform"></a>关于平台

Windows 传感器和位置平台由以下开发人员和用户组件构成：

- DDI。 Windows 提供了一种连接传感设备与计算机以及传感设备用于向其他子系统提供数据的标准方式。

- Windows 传感器 API 提供了一组用于处理连接的传感器和传感器数据的方法、属性和事件。

- 基于 Windows 传感器 API 构建的 Windows 位置 API 提供一组编程对象。 这些对象中包括处理位置信息的脚本对象。

- 通过“控制面板”，计算机用户能够控制位置设置。

以下各部分对上述各组件进行了介绍。

### <a name="device-driver-interface"></a>设备驱动程序接口

传感器制造商可以创建将传感器连接到 Windows 的设备驱动程序。 传感器设备驱动程序通过使用 Windows 便携设备 (WPD) 驱动程序模型实现，该模型基于 Windows 用户模式驱动程序框架 (UMDF)。许多设备驱动程序都是使用这些框架编写的。 由于这些技术已十分成熟，因此经验丰富的设备驱动程序程序员对编写传感器驱动程序不会感到陌生。 传感器 DDI 使用特定 UMDF 和 WPD 数据类型和接口，并在需要时定义特定于传感器的 WPD 命令和参数。

为了更便于编写向 Windows 公开传感器（特别是向传感器和位置平台公开）的设备驱动程序，操作系统包含了一个驱动程序类扩展。 此 COM 对象是传感器设备驱动程序的必备组件，提供一组简单的接口，使程序员无需编写大量样板代码就能够实现传感器驱动程序。 类扩展还可以减少（甚至消除）管理 WPD 调用的需求。 此文档包含有关传感器 DDI 和类扩展对象的详细信息。

### <a name="sensor-api"></a>传感器 API

使用 Windows 传感器 API，C++ 开发人员可以通过使用一组 COM 接口来创建基于传感器的程序。 API 定义用于执行常见传感器编程任务的接口，这些任务包括按类别、类型或 ID 管理传感器、管理传感器事件、使用单个传感器和传感器集合以及处理传感器数据。 Windows SDK 包括头文件、文档、示例和工具，可帮助软件开发人员了解如何使用 Windows 程序中的传感器。

### <a name="location-api"></a>位置 API

位置 API 是基于传感器平台构建的，它提供了一种简单的方法来检索有关地理位置的数据，同时保护用户隐私。 位置 API 通过一组表示对象的 COM 接口提供其功能。 了解如何通过 C++ 编程语言或在脚本语言（如 JScript）中使用 COM 的程序员可以利用这些对象来完成工作。 借助脚本支持，本地计算机区域中运行的项目（如小工具）便能够轻松访问位置数据。 Windows SDK 包括头文件、文档（包括脚本参考文档）、示例和工具，可帮助 Web 和软件开发人员了解如何在其程序中使用位置信息。

### <a name="user-control-panel"></a>用户控制面板

Windows 包括一个控制面板，计算机用户通过它能够启用或禁用位置设置。 由于这些设置可以公开敏感数据，因此用户能够通过此用户界面控制某个程序是否有权访问其位置。

## <a name="whitepapers"></a>白皮书

| Title | 描述 |
| -- | -- |
| [HID 传感器的使用](/windows-hardware/design/whitepapers/hid-sensors-usages) | 本白皮书提供了有关 Windows 8 及更高版本操作系统的 HID 传感器类驱动程序的信息。 |
| [将氛围光传感器与运行 Windows 10 创意者更新的计算机集成](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) | 本白皮书提供了有关 Windows 10 操作系统的环境光线传感器 (ALS) 功能的信息。  |
| [集成动作和方向传感器](/windows-hardware/design/whitepapers/integrating-motion-and-orientation-sensors) | 本白皮书的目的是帮助 OEM、ODM 和 IHV 了解 Windows 10 及早期操作系统的动作和方向传感器功能和要求。 |

## <a name="related-sections"></a>相关章节

- [传感器 DDI 参考](/windows-hardware/drivers/ddi/_sensors/)
- [传感器博客](https://techcommunity.microsoft.com/t5/microsoft-sensors-blog/bg-p/MicrosoftSensorsBlog)
