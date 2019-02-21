---
title: 组合提供程序扩展
description: 组合提供程序扩展
ms.assetid: 94F73ECD-54D0-4218-B3C4-33DC3BD57ED0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac8019547ac19006c46433307eb0ce9c75ecf37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544149"
---
# <a name="teaming-provider-extensions"></a>组合提供程序扩展


可扩展交换机外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 在主机上，MUX 中间驱动程序本身可以绑定到一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展公开到可扩展交换机团队中每个网络适配器。 这样，转发扩展中要管理的配置和使用的团队中的单个网络适配器的可扩展交换机驱动程序堆栈。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 此类扩展被称为*组合的提供程序*。

下图显示了与绑定到外部网络适配器的 NDIS 6.40 (Windows Server 2012 R2) 及更高版本的基础可扩展交换机团队的数据包流量的数据路径。

![与绑定到外部网络适配器的 ndis 6.40 vswitch 团队的数据包流量的数据路径](images/vswitchteam-ndis640.png)

下图显示了与的 NDIS 6.30 (Windows Server 2012) 绑定到外部网络适配器的基础可扩展交换机团队的数据包流量的数据路径。

![与绑定到外部网络适配器的 ndis 6.30 vswitch 团队的数据包流量的数据路径](images/vswitchteam.png)

组合提供程序可以执行所有操作可以转发扩展。 此外，组合提供程序可以执行以下操作。

-   将传出数据包转发到可扩展交换机团队中的各个物理适配器。 此功能对于 LBFO 功能特别有用。

-   标准 NDIS 对象标识符 (OID) 将请求转发到可扩展交换机团队中的各个物理适配器。 此功能是在硬件卸载功能的团队中配置适配器的特别有用。

    例如，MUX 驱动程序会通告整个可扩展交换机团队的常见功能。 但是，组合的提供程序可以发出 OID 请求，可查询的适配器在团队中的各个功能。 然后，组合的提供程序可以发出 OID 请求到可扩展交换机外部网络适配器设置将应用于整个团队的功能。

-   将私有 OID 请求转发到可扩展交换机团队中的各个物理适配器。 这些专用的 OID 请求由物理网络适配器的独立硬件供应商 (IHV) 定义。 这样的组合提供程序也由 IHV 可以启用或禁用在团队中的各个物理适配器的专有特性。

-   修改可扩展交换机团队 NDIS 状态指示。 此功能是用于管理硬件卸载功能的可扩展交换机团队特别有用。

    例如，MUX 驱动程序问题常见的整个可扩展交换机团队设置 NDIS 状态的指示。 如果状态指示已针对硬件卸载为可扩展交换机团队中的网络适配器成组提供程序启用的组合的提供程序可以首先发出 OID 请求来查询该适配器上的当前功能。 然后，组合的提供程序可以修改要在适配器上设置可能已更改这些属性指示数据。

管理可扩展交换机团队时，组合提供程序必须遵循以下准则：

-   组合的提供程序必须保持为不可扩展交换机的网络连接必须为其建立每个物理网络适配器的状态。

    有关每个绑定到外部网络适配器的物理网络适配器，可扩展交换机的协议边缘问题的一个单独的 OID 集请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)。 此 OID 请求通知有关与基础物理适配器的网络连接创建的扩展。

-   创建与物理网络适配器的网络连接时，它分配对外部网络适配器连接到的端口都是唯一一个非零的索引值。

    时或者将数据包或 OID 请求转发到基础物理网络适配器成组提供程序必须指定网络适配器索引值。

    有关详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

-   如果组合提供程序问题，或将数据包转发到的物理适配器，它必须指定连接的物理适配器的非零的网络适配器索引值。

    当提供程序接收数据包时，它可以确定从数据包的带外转发上下文中的源网络适配器索引值[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 有关转发上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

    有关详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

-   若要发出的物理适配器的 OID 将请求转发，组合的提供程序必须封装 OID 请求内的[ **NDIS\_交换机\_NIC\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh598214)结构。 提供程序必须设置**DestinationNicIndex**为非零的网络适配器的索引值的物理适配器连接的成员。 然后提供者所颁发的 OID 集请求[OID\_交换机\_NIC\_请求](https://msdn.microsoft.com/library/windows/hardware/hh598266)将封装的 OID 请求传递到目标物理适配器。

    有关详细信息，请参阅[到物理网络适配器管理 OID 请求](managing-oid-requests-to-physical-network-adapters.md)。

-   组合的提供程序可以发出代表基础物理适配器的 NDIS 状态指示。 若要执行此操作，该提供程序必须封装中的指示[ **NDIS\_交换机\_NIC\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/hh598217)结构。 提供程序必须设置**SourceNicIndex**为非零的网络适配器的索引值的物理适配器连接的成员。 然后，该提供程序发出的 NDIS 状态指示[ **NDIS\_状态\_交换机\_NIC\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598205)提供封装的状态指示到过量可扩展交换机驱动程序堆栈中的驱动程序。

    有关详细信息，请参阅[从物理网络适配器管理 NDIS 状态指示](managing-ndis-status-indications-from-physical-network-adapters.md)。

有关转发扩展的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





