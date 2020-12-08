---
title: UMDF 概述
description: 本主题提供了有关 UMDF 组件的高级概述，并介绍了驱动程序如何与系统提供的组件交互。
keywords:
- User-Mode Driver Framework WDK，关于 UMDF
- UMDF WDK，关于 UMDF
- 用户模式驱动程序 WDK UMDF，关于 UMDF
- 驱动程序主机进程 WDK UMDF
- 发送程序 WDK UMDF
- 驱动程序管理器 WDK UMDF
- 堆栈 WDK UMDF
- 设备堆栈 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c7b8b2f17ed8a635bf709c8c7c944461d0d80ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795777"
---
# <a name="overview-of-umdf"></a>UMDF 概述


本主题概述了 User-Mode Driver Framework (UMDF) 组件，并介绍了驱动程序如何与系统提供的组件交互。 它适用于 UMDF 版本1和2。

UMDF 驱动程序抽象硬件功能，在用户模式环境中运行，并且可以访问不同的服务。 UMDF 驱动程序作为管理设备的驱动程序堆栈的一部分运行。 文件系统驱动程序，显示完整显示设备 (的驱动程序，而不显示仅显示的显示设备) ，打印驱动程序不能是 UMDF 驱动程序。

UMDF 驱动程序与以下系统提供的组件交互：

-   驱动程序主机进程

    驱动程序主机进程加载供应商提供的 UMDF 驱动程序和框架 Dll，提供用户模式驱动程序的执行环境，并在用户模式堆栈中的驱动程序之间路由消息。 有关详细信息，请参阅 [UMDF 驱动程序主机进程](umdf-driver-host-process.md)。

-   驱动程序管理器

    驱动程序管理器是一种 Windows 服务，用于管理 Wudfhost 驱动程序主机进程的所有实例。 驱动程序管理器将启动和跟踪有关每个驱动程序主机进程的信息。 每个主机都是驱动程序管理器的子进程。 每个系统只存在一个驱动程序管理器。 驱动程序管理器将在安装第一个 UMDF 设备时启动，之后在系统上运行。

-   Reflector

    反射器是一个内核模式驱动程序，它允许应用程序和驱动程序主机进程 (，并) 用户模式的设备堆栈进行通信。 反射器为每个设备实例创建一个单独的设备对象，并处理与每个设备实例关联的即插即用 (PnP) 和电源 i/o 请求。 应用程序和驱动程序主机进程之间的所有通信都通过反射器进行。 有关详细信息，请参阅 [UMDF 的体系结构](detailed-view-of-the-umdf-architecture.md)。

给定设备的所有函数和筛选器驱动程序必须在同一驱动程序主机进程中运行，但可以同时运行多个主机进程。

下图显示了驱动程序主机进程、驱动程序管理器和反射器如何在用户模式/内核模式边界之间进行通信。

![umdf 组件在反射器中包含向上和向下设备对象](images/umdfarch3.gif)

 

 





