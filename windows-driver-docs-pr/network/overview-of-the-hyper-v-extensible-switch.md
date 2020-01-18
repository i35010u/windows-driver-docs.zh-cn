---
title: Hyper-V 可扩展交换机概述
description: 本部分概述了 Hyper-v 可扩展交换机
ms.assetid: 78181C72-FBFD-4860-A664-C297997D780F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9a7433ef16457a9a9e5844b5eb9d894490efd38
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256757"
---
# <a name="overview-of-the-hyper-v-extensible-switch"></a>Hyper-V 可扩展交换机概述

Windows Server 2012 引入了 Hyper-v 可扩展交换机（也称为 Hyper-v 虚拟交换机），这是在 Hyper-v 父分区的管理操作系统中运行的虚拟以太网交换机。 本页介绍了以下主题：

- [背景阅读](#background-reading)
- [Hyper-v 可扩展交换机和网络适配器的类型](#types-of-hyper-v-extensible-switches-and-network-adapters)
- [可扩展交换机扩展的类型](#types-of-extensible-switch-extensions)
- [Hyper-v 可扩展交换机体系结构关系图](#hyper-v-extensible-switch-architectural-diagrams)

## <a name="background-reading"></a>背景阅读

有关此技术及其 connect-through 的高级技术概述，请参阅以下 TechNet 文档：

- [Hyper-V 虚拟交换机概述](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831823(v=ws.11))
- [Hyper-V 网络虚拟化概述](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134230(v=ws.11))
- [Hyper-v 概述](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))

## <a name="types-of-hyper-v-extensible-switches-and-network-adapters"></a>Hyper-v 可扩展交换机和网络适配器的类型

Hyper-v 虚拟网络管理器可用于创建、配置或删除以下类型的一个或多个可扩展交换机：

- 支持连接到单个外部网络适配器的端口以及一个或多个虚拟机（VM）网络适配器的外部可扩展交换机。 此类型的开关允许在所有 Hyper-v 分区与主机上的物理网络接口之间发送或接收数据包。

    此外，在管理操作系统中运行的应用程序和驱动程序可以通过此类型的开关发送或接收数据包。

- 支持连接到一个或多个内部网络适配器以及一个或多个 VM 网络适配器的端口的内部可扩展交换机。 此类型的开关允许在 Hyper-v 父分区与主机上的一个或多个 Hyper-v 子分区之间发送或接收数据包。

    此外，在管理操作系统中运行的应用程序和驱动程序可以通过此类型的开关发送或接收数据包。

- 支持连接到一个或多个 VM 网络适配器的端口的专用可扩展交换机。 此类型的开关允许仅在 Hyper-v 子分区之间发送或接收数据包。

    **注意**  在管理操作系统中运行的应用程序和驱动程序无法通过此类型的开关发送或接收数据包。

每个可扩展交换机模块都通过 Hyper-v 子分区和父分区使用的网络适配器来路由传入和传出数据包。 这些网络适配器包括：

- 外部网络适配器，提供与主机上可用的物理网络接口的连接。

    有关此类网络适配器的详细信息，请参阅[外部网络适配器](https://docs.microsoft.com/windows-hardware/drivers/network/external-network-adapters)。

    **请注意**  仅外部可扩展交换机提供对外部网络适配器的访问权限。

- 内部网络适配器，为在 Hyper-v 父分区的管理操作系统中运行的进程提供对可扩展交换机的访问。 这允许这些进程通过可扩展交换机发送或接收数据包。

    有关此类网络适配器的详细信息，请参阅[内部网络适配器](https://docs.microsoft.com/windows-hardware/drivers/network/internal-network-adapters)。

    **请注意**  仅外部和内部可扩展交换机提供对内部网络适配器的访问权限。

- 在 Hyper-v 子分区中运行的来宾操作系统内公开的 VM 网络适配器。 VM 网络适配器提供了到可扩展交换机的连接，这些数据包由在子分区的来宾操作系统中运行的进程发送或接收。

    有关此类网络适配器的详细信息，请参阅[虚拟机网络适配器](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-network-adapters)。

每个 Hyper-v 子分区都可以配置为具有一个或多个 VM 网络适配器。 每个 VM 网络适配器都配置为与可扩展交换机的一个实例相关联。 这允许按以下方式配置子分区：

- 可以将子分区配置为具有与可扩展交换机的一个实例相关联的单个 VM 网络适配器。

- 子分区可配置为具有多个 VM 网络适配器，每个 VM 网络适配器与一个可扩展交换机的实例关联。

- 子分区可以配置为具有多个 VM 网络适配器，其中一个或多个 VM 网络适配器与一个可扩展交换机的同一个实例相关联。

## <a name="types-of-extensible-switch-extensions"></a>可扩展交换机扩展的类型

Hyper-v 可扩展交换机支持独立软件供应商（Isv）可通过以下方式扩展交换机功能的接口：

- Hyper-v 可扩展交换机支持一个接口，该接口允许将 NDIS 筛选器驱动程序（称为 "*扩展*"）绑定到可扩展交换机驱动程序堆栈中。 这允许扩展插件捕获、筛选和转发数据包到可扩展的交换机端口。 这还允许扩展插件将数据包注入、删除或重定向到连接到 Hyper-v 分区中公开的网络适配器的端口。

    安装扩展后，可以在 Hyper-v 可扩展交换机的单独实例上启用或禁用它们。 有关详细信息，请参阅[安装 Hyper-v 可扩展交换机扩展](https://docs.microsoft.com/windows-hardware/drivers/network/installing-hyper-v-extensible-switch-extensions)。

- Windows 筛选平台（WFP）提供了一个内置筛选扩展（Wfplwfs），它允许 WFP 筛选器或标注驱动程序沿 Hyper-v 可扩展交换机数据路径截获数据包。 这允许 WFP 筛选器或标注驱动程序使用 WFP 管理和系统函数执行数据包检查或修改。

    有关 WFP 的概述，请参阅[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/network/porting-packet-processing-drivers-and-apps-to-wfp)。

    有关 WFP 标注驱动程序的概述，请参阅[Windows 筛选平台标注驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)。

    **请注意**  要对可扩展交换机数据包流量执行基于 WFP 的筛选，isv 只需扩展其 WFP 筛选器和标注驱动程序以使用扩展的 wfp 调用和数据类型。 Isv 无需开发自己的扩展。

可扩展交换机接口支持以下类型的扩展：

<a href="" id="capturing-extensions"></a>捕获扩展  
捕获和监视数据包流量的扩展。 这种类型的扩展不能修改或丢弃数据包，也不能排除数据包被传递到可扩展交换机端口。 但是，捕获扩展可能会产生数据包流量，例如包含扩展发送到主机应用程序的流量统计信息的数据包。

在可扩展交换机的每个实例中，可以绑定和启用多个捕获扩展。

有关此类型的扩展的详细信息，请参阅[捕获扩展](https://docs.microsoft.com/windows-hardware/drivers/network/capturing-extensions)。

<a href="" id="filtering-extensions"></a>筛选扩展  
这些扩展具有与捕获扩展相同的功能。 但是，这种类型的扩展可以基于端口或交换机策略设置来检查和丢弃数据包，或排除数据包传递到可扩展的交换机端口。 筛选扩展还可以发起、复制或克隆数据包，并将其插入可扩展交换机数据路径。

在可扩展交换机的每个实例中，可以绑定和启用多个筛选扩展。

有关此类型的扩展的详细信息，请参阅[筛选扩展](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-extensions)。

<a href="" id="forwarding-extensions"></a>转发扩展  
这些扩展与筛选扩展具有相同的功能，但负责执行核心数据包转发和可扩展交换机的筛选任务。 这些任务包括以下内容：

- 确定数据包的目标端口，除非数据包为 NVGRE 数据包。 有关详细信息，请参阅[混合转发](https://docs.microsoft.com/windows-hardware/drivers/network/hybrid-forwarding)。

- 通过强制实施标准端口策略来筛选数据包，如安全性、配置文件或虚拟 LAN （VLAN）策略。

**请注意**  如果未在可扩展交换机中安装和启用转发扩展，则交换机会确定数据包的目标端口，并根据标准端口设置筛选数据包。

在可扩展交换机的每个实例中只能绑定和启用一个转发扩展。

有关此类型的扩展的详细信息，请参阅[转发扩展](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-extensions)。

## <a name="hyper-v-extensible-switch-architectural-diagrams"></a>Hyper-v 可扩展交换机体系结构关系图

下图显示了 NDIS 6.40 （Windows Server 2012 R2）和更高版本的可扩展交换机接口的组件。

![说明 ndis 6.40 和更高版本的超级\-v 可扩展交换机体系结构的示意图](images/vswitcharchitecture-ndis640.png)

下图显示了用于 NDIS 6.30 的可扩展交换机接口（Windows Server 2012）的组件。

![用 sr-iov 说明综合设备数据路径的示意图](images/vswitcharchitecture.png)

有关可扩展交换机接口的组件的详细信息，请参阅[Hyper-v 可扩展交换机体系结构](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-architecture)。
