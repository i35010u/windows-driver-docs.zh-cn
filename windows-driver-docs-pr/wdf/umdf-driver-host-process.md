---
title: UMDF 驱动程序主机进程
description: 本主题介绍用户模式驱动程序框架 (UMDF) 驱动程序主机进程及其使用方式与其他 UMDF 组件。 它适用于这两种 UMDF 版本 1 和 2。
ms.assetid: 8b469c91-d33d-4fb0-8c7d-e90f86a1e339
keywords:
- 驱动程序主机进程 WDK UMDF
- 用户模式驱动程序框架 WDK，体系结构
- UMDF WDK，体系结构
- 用户模式驱动程序 WDK UMDF，体系结构
- 体系结构 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c32486dfe75292f29c2e34fb807574f8ecc0fff4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523591"
---
# <a name="umdf-driver-host-process"></a>UMDF 驱动程序主机进程


本主题介绍用户模式驱动程序框架 (UMDF) 驱动程序主机进程及其使用方式与其他 UMDF 组件。 它适用于这两种 UMDF 版本 1 和 2。

驱动程序主机进程 (Wudfhost.exe) 是驱动程序管理器服务的一个子过程。 在通常运行 Wudfhost.exe *LocalService*在本地计算机具有最小特权的帐户。 Wudfhost.exe 的实例加载一个或多个 UMDF 驱动程序 Dll，除了框架的 Dll。 驱动程序主机进程之间驱动程序管理器和发送程序，以及 I/O 调度、 驱动程序加载、 驱动程序分层和线程池管理提供了处理进程间通信 (IPC) 的运行时环境。

驱动程序管理器可以创建多个并发实例 Wudfhost.exe，如下所示：

-   如果 UMDF 驱动程序版本 1.11 用生成以及 Windows 8 上运行，默认情况下将驱动程序管理器创建 Wudfhost 可以托管多个设备堆栈的单个实例。 这一技术称为*设备池*。

    如果 UMDF 驱动程序已使用版本 2 构建，并在 Windows 8.1 或 Windows 10 上运行，池也是在默认情况下。

-   如果您的驱动程序已使用 UMDF 1.9 或更早版本生成的框架将创建每个设备堆栈的主机进程 (Wudfhost) 的单独实例。

有关设备池的详细信息，请参阅[UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

内 Wudfhost.exe，每个 UMDF 驱动程序在自己的地址空间中运行，因此是独立于应用程序和驱动程序主机的其他实例。

您可以加载驱动程序使用 UMDF 版本 1 和 2 同时，在相同的主机进程或不同的宿主进程中生成。 例如，默认情况下，驱动程序管理器会加载一个 UMDF 1.11 的驱动程序和运行 Windows 8.1 或更高版本的计算机上的相同主机进程中的 UMDF 2 驱动程序。

但是，无法加载 UMDF 版本 1 和 2 相同的设备堆栈中的驱动程序。 例如，无法加载 UMDF 版本 1 的筛选器驱动程序上面 UMDF 版本 2 功能驱动程序。

显示驱动程序主机如何与其他 UMDF 组件相关联的关系图，请参阅[UMDF 概述](overview-of-the-umdf.md)。

 

 





