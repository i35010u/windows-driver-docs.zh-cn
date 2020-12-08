---
title: UMDF 驱动程序主机进程
description: 本主题介绍 User-Mode Driver Framework (UMDF) 驱动程序主机进程，以及它如何与其他 UMDF 组件配合使用。 它适用于 UMDF 版本1和2。
keywords:
- 驱动程序主机进程 WDK UMDF
- User-Mode Driver Framework WDK、体系结构
- UMDF WDK，体系结构
- 用户模式驱动程序 WDK UMDF、体系结构
- 体系结构 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 090f5b1bd2c7ffaae8ab2117278ff1533a53a3a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96781996"
---
# <a name="umdf-driver-host-process"></a>UMDF 驱动程序主机进程


本主题介绍 User-Mode Driver Framework (UMDF) 驱动程序主机进程，以及它如何与其他 UMDF 组件配合使用。 它适用于 UMDF 版本1和2。

驱动程序主机进程 ( # A0) 是驱动程序管理器服务的子进程。 Wudfhost.exe 通常在 *LocalService* 帐户中运行，该帐户在本地计算机上具有最小权限。 除了框架 Dll 外，Wudfhost.exe 的实例还会加载一个或多个 UMDF 驱动程序 Dll。 驱动程序主机进程提供一个运行时环境，该环境处理驱动程序管理器和反射器之间 (IPC) 的进程间通信，以及 i/o 调度、驱动程序加载、驱动程序分层和线程池管理。

驱动程序管理器可以创建 Wudfhost.exe 的多个并发实例，如下所示：

-   如果 UMDF 驱动程序是使用版本1.11 生成的，并且在 Windows 8 上运行，则默认情况下，驱动程序管理器会创建一个可托管多个设备堆栈的 Wudfhost 实例。 此方法称为 *设备池*。

    如果 UMDF 驱动程序是使用版本2构建的，并且在 Windows 8.1 或 Windows 10 上运行，则默认情况下，池也处于启用状态。

-   如果驱动程序是使用 UMDF 1.9 版或更早版本生成的，则框架将为每个设备堆栈 (Wudfhost) 创建一个单独的主机进程实例。

有关设备池的详细信息，请参阅 [在 UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

在 Wudfhost.exe 中，每个 UMDF 驱动程序都在其自己的地址空间中运行，因此独立于应用程序进程和驱动程序主机的其他实例。

可以在同一主机进程或不同的主机进程中，同时加载用 UMDF 版本1和2生成的驱动程序。 例如，默认情况下，驱动程序管理器将在运行 Windows 8.1 或更高版本的计算机上的同一主机进程中加载一个 UMDF 1.11 驱动程序和一个 UMDF 2 驱动程序。

但是，不能在同一设备堆栈中加载 UMDF 版本1和2驱动程序。 例如，你不能在 UMDF 版本2功能驱动程序之上加载 UMDF 版本1筛选器驱动程序。

有关显示驱动程序主机如何与其他 UMDF 组件相关的关系图，请参阅 [UMDF 概述](overview-of-the-umdf.md)。

 

 





