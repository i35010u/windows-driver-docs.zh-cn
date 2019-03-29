---
title: UMDF 概述
description: 本主题提供 UMDF 组件的高级概述，并介绍了您的驱动程序如何与系统提供的组件进行交互。
ms.assetid: b36c9fad-1963-4d29-a1e7-890de77fed50
keywords:
- 用户模式驱动程序框架 WDK，有关 UMDF
- UMDF WDK，有关 UMDF
- 用户模式驱动程序 WDK UMDF，有关 UMDF
- 驱动程序主机进程 WDK UMDF
- 发送程序 WDK UMDF
- 驱动程序管理器 WDK UMDF
- 堆栈 WDK UMDF
- 设备堆栈 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92d7edbe76a1a8bd8a77d4e1ca0a685583e79656
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577178"
---
# <a name="overview-of-umdf"></a>UMDF 概述


本主题提供用户模式驱动程序框架 (UMDF) 组件的高级概述，并介绍了您的驱动程序如何与系统提供的组件进行交互。 它适用于这两种 UMDF 版本 1 和 2。

UMDF 驱动程序抽象硬件功能，运行在用户模式环境中，并且可以访问各种服务。 UMDF 驱动程序采用的管理设备的驱动程序堆栈的一部分运行。 文件系统驱动程序、 （适用于完整的显示设备不仅显示显示设备） 使用，显示器驱动程序和打印驱动程序不能为 UMDF 驱动程序。

UMDF 驱动程序与系统提供的以下组件进行交互：

-   驱动程序主机进程

    驱动程序主机进程加载供应商提供 UMDF 驱动程序和框架的 Dll、 提供执行环境，用于用户模式驱动程序和用户模式堆栈中的驱动程序之间路由消息。 有关详细信息，请参阅[UMDF 驱动程序主机进程](umdf-driver-host-process.md)。

-   驱动程序管理器

    驱动程序管理器是用于管理 Wudfhost 驱动程序主机进程的所有实例的 Windows 服务。 驱动程序管理器启动并跟踪每个驱动程序主机进程有关的信息。 每个主机是驱动程序管理器的子进程。 只有一个驱动程序管理器存在每个系统。 驱动程序管理器在第一台 UMDF 设备安装过程中启动，并在系统上之后运行。

-   反射器

    该发送程序是一个内核模式驱动程序允许应用程序和驱动程序主机进程 （和用户模式设备堆栈） 进行通信。 该发送程序创建单独的设备对象的每个设备实例和句柄插 (PnP) 以及与每个设备实例相关联的电源 I/O 请求。 应用程序和驱动程序主机进程之间的所有通信都是通过反射器。 有关详细信息，请参阅[体系结构的 UMDF](detailed-view-of-the-umdf-architecture.md)。

为给定设备的所有函数和筛选器驱动程序必须都运行相同的驱动程序主机进程中，但可以同时运行多个主机进程。

下图显示了跨用户模式/内核模式下边界驱动程序主机进程、 驱动程序管理器和反射的进行通信。

![umdf 组件包括向上和向下发送程序中的设备对象](images/umdfarch3.gif)

 

 





