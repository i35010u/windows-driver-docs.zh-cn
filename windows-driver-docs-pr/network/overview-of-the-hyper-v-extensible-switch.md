---
title: HYPER-V 可扩展交换机的概述
description: 本部分概述的 HYPER-V 可扩展交换机
ms.assetid: 78181C72-FBFD-4860-A664-C297997D780F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ef4da2acff5012ec9f058c1f29aaa7bc1eb4ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519491"
---
# <a name="overview-of-the-hyper-v-extensible-switch"></a>HYPER-V 可扩展交换机的概述


Windows Server 2012 引入的 HYPER-V 可扩展交换机 （也称为 HYPER-V 虚拟交换机），这是在 HYPER-V 父分区的管理操作系统中运行的虚拟以太网交换机。 此页包含以下主题：

-   [背景读取](#background-reading)
-   [类型的 HYPER-V 可扩展交换机和网络适配器](#types-of-hyper-v--extensible-switches-and-network-adapters)
-   [类型的可扩展交换机扩展](#types-of-extensible-switch-extensions)
-   [HYPER-V 可扩展交换机体系结构关系图](#hyper-v-extensible-switch-architectural-diagrams)

## <a name="background-reading"></a>背景读取


有关此技术和其基础的高级技术概述，请参阅以下 TechNet 文档：

-   [Hyper-V 虚拟交换机概述](https://technet.microsoft.com/library/hh831823.aspx)
-   [Hyper-V 网络虚拟化概述](https://technet.microsoft.com/library/jj134230.aspx)
-   [HYPER-V 概述](https://technet.microsoft.com/library/hh831531.aspx)

## <a name="types-of-hyper-v-extensible-switches-and-network-adapters"></a>类型的 HYPER-V 可扩展交换机和网络适配器


HYPER-V 虚拟网络管理器可以用于创建、 配置或删除以下类型的一个或多个可扩展交换机：

-   外部可扩展交换机支持连接到一个外部网络适配器，以及一个或多个虚拟机 (VM) 网络适配器的端口。 此类型的交换机允许将数据包发送或接收的 HYPER-V 的所有分区和主机上的物理网络接口之间。

    此外，应用程序和管理操作系统中运行的驱动程序可以发送或接收通过此类型的交换机的数据包。

-   内部可扩展交换机支持连接到一个或多个内部网络适配器，以及一个或多个 VM 网络适配器的端口。 此类型的交换机允许将数据包发送或接收的 HYPER-V 父分区和在主机上的一个或多个 HYPER-V 子分区之间。

    此外，应用程序和管理操作系统中运行的驱动程序可以发送或接收通过此类型的交换机的数据包。

-   专用的可扩展交换机支持连接到一个或多个 VM 网络适配器的端口。 此类型的交换机允许将数据包发送或接收仅之间的 HYPER-V 子分区。

    **请注意**  应用程序和管理操作系统中运行的驱动程序无法发送或接收通过此类型的交换机的数据包。

     

每个可扩展交换机模块通过 HYPER-V 子和父分区使用的网络适配器将路由传入和传出数据包。 这些网络适配器包括：

-   提供到主机上可用的物理网络接口的连接的外部网络适配器。

    有关此类型的网络适配器的详细信息，请参阅[外部的网络适配器](external-network-adapters.md)。

    **请注意**  仅外部可扩展交换机提供对外部网络适配器的访问权限。

     

-   提供对可扩展交换机的 HYPER-V 父分区在管理操作系统中运行的进程的访问权限的内部网络适配器。 这允许这些进程发送或接收通过可扩展交换机的数据包。

    有关此类型的网络适配器的详细信息，请参阅[内部网络适配器](internal-network-adapters.md)。

    **请注意**  仅外部和内部可扩展交换机提供对内部网络适配器的访问权限。

     

-   公开运行 HYPER-V 子分区中的来宾操作系统中的 VM 网络适配器。 VM 网络适配器提供的连接到可扩展交换机的数据包，以发送或接收的子分区的来宾操作系统中运行的进程。

    有关此类型的网络适配器的详细信息，请参阅[虚拟机网络适配器](virtual-machine-network-adapters.md)。

每个 HYPER-V 子分区可以配置为具有一个或多个 VM 网络适配器。 每个 VM 网络适配器配置为与可扩展交换机的实例相关联。 这允许子分区以配置如下所示：

-   子分区可以配置为具有与可扩展交换机的一个实例相关联的单一 VM 网络适配器。

-   子分区可以配置为具有多个 VM 网络适配器，与每个 VM 网络适配器与可扩展交换机的实例相关联。

-   子分区可以配置为具有多个 VM 网络适配器，与一个或多个 VM 网络适配器与可扩展交换机的同一个实例相关联。

## <a name="types-of-extensible-switch-extensions"></a>类型的可扩展交换机扩展


HYPER-V 可扩展交换机支持在其中独立软件供应商 (Isv) 可以按以下方式扩展交换机功能的接口：

-   HYPER-V 可扩展交换机支持的接口可用于 NDIS 筛选器驱动程序，称为*扩展*、 要在可扩展交换机驱动程序堆栈中绑定。 这允许扩展到捕获、 筛选和可扩展交换机端口转发数据包。 这也允许扩展来插入、 删除或重定向到已连接到在 HYPER-V 分区中公开的网络适配器的端口的数据包。

    安装扩展后，它们可以启用或禁用 HYPER-V 可扩展交换机的不同实例上。 有关详细信息，请参阅[安装的 HYPER-V 可扩展交换机扩展](installing-hyper-v-extensible-switch-extensions.md)。

-   Windows 筛选平台 (WFP) 提供了允许 WFP 筛选器或标注驱动程序来截获的 HYPER-V 可扩展交换机数据路径上的数据包的框中筛选扩展 (Wfplwfs.sys)。 这样的 WFP 筛选器或标注驱动程序来执行数据包检查或修改使用 WFP 管理和系统函数。

    有关 WFP 的概述，请参阅[Windows 筛选平台](porting-packet-processing-drivers-and-apps-to-wfp.md)。

    WFP 标注驱动程序的概述，请参阅[Windows 筛选平台标注驱动程序](windows-filtering-platform-callout-drivers2.md)。

    **请注意**  若要执行基于 WFP 的可扩展交换机数据包流量的筛选，Isv 只需扩展其 WFP 筛选并标注驱动程序以使用扩展 WFP 调用和数据类型。 Isv 不必开发自己的扩展。

     

可扩展交换机接口支持以下类型的扩展：

<a href="" id="capturing-extensions"></a>捕获扩展  
捕获并监视数据包流量的扩展。 此类型的扩展不能修改或丢弃的数据包，或从正被传递到可扩展的交换机端口中排除的数据包。 但是，捕获扩展可以源自数据包流量，例如包，其中包含扩展将发送到主机应用程序的流量统计数据。

可以绑定并在可扩展交换机的每个实例中启用多个捕获扩展。

此类扩展的详细信息，请参阅[捕获扩展](capturing-extensions.md)。

<a href="" id="filtering-extensions"></a>筛选扩展  
这些扩展具有与捕获扩展相同的功能。 但是，根据端口或交换机策略设置，此类扩展可以检查和丢弃的数据包，或排除的数据包发送到可扩展交换机端口。 筛选扩展可以还源自、 重复的或克隆数据包并将其注入到可扩展交换机数据路径。

可以绑定并在可扩展交换机的每个实例中启用多个筛选扩展。

此类扩展的详细信息，请参阅[筛选扩展](filtering-extensions.md)。

<a href="" id="forwarding-extensions"></a>转发扩展  
这些扩展具有相同的功能作为筛选扩展，但负责执行核心数据包转发和筛选的可扩展交换机的任务。 这些任务包括：

-   确定数据包的目标端口，除非该数据包是 NVGRE 数据包。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

-   通过强制执行标准端口的策略，如安全、 配置文件或虚拟 LAN (VLAN) 策略筛选数据包。

**请注意**  转发扩展未安装和启用了可扩展的交换机中，如果交换机确定数据包的目标端口以及筛选器基于标准的端口设置的数据包。

 

可以绑定并启用了可扩展交换机的每个实例中只有一个转发扩展。

此类扩展的详细信息，请参阅[转发扩展](filtering-extensions.md)。

## <a name="hyper-v-extensible-switch-architectural-diagrams"></a>HYPER-V 可扩展交换机体系结构关系图


下图显示了可扩展交换机接口 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的组件。

![关系图阐释超\-ndis 6.40 及更高版本的 v 可扩展交换机体系结构](images/vswitcharchitecture-ndis640.png)

下图显示了可扩展交换机接口的组件的 NDIS 6.30 (Windows Server 2012)。

![说明与 sr-iov 的合成设备数据路径的关系图](images/vswitcharchitecture.png)

有关可扩展交换机接口的组件的详细信息，请参阅[HYPER-V 可扩展交换机体系结构](hyper-v-extensible-switch-architecture.md)。

 

 





