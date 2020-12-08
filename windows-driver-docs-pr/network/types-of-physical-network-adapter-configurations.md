---
title: 物理网络适配器配置的类型
description: 物理网络适配器配置的类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0cd51df26e067d7dc5bed658281e82a4d5cdbb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815859"
---
# <a name="types-of-physical-network-adapter-configurations"></a>物理网络适配器配置的类型


Hyper-v 可扩展交换机体系结构支持与单个外部网络适配器的连接，以访问基础物理介质。 外部网络适配器可以绑定到以下物理网络适配器配置之一：

-   外部网络适配器可以绑定到一个基础物理网络适配器。 在此配置中，可扩展交换机扩展会暴露到主机上，并且仅管理一个基础网络适配器。

    下图显示了一个可扩展交换机配置，其中的外部网络适配器绑定到用于 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的单个物理网络适配器。

    ![使用外部网络适配器绑定到 ndis 6.40 和更高版本的单一物理网络适配器的 vswitch 配置](images/vswitchsingle-ndis640.png)

    下图显示了一个可扩展交换机配置，其中的外部网络适配器绑定到用于 NDIS 6.30 (Windows Server 2012) 的单个物理网络适配器。

    ![使用外部网络适配器绑定到 ndis 6.30 的单个物理网络适配器的 vswitch 配置](images/vswitchsingle.png)

-   可以将外部网络适配器绑定到负载均衡故障转移 (LBFO) 提供程序的虚拟微型端口边缘。 这是一个 ndis 筛选器驱动程序，它在 NDIS 多路复用器 (MUX) 驱动程序上分层，该驱动程序可以绑定到主机上的一个或多个物理网络的团队。 此配置称为 *LBFO 团队*。

    在此配置中，可扩展交换机扩展仅向网络适配器公开基础虚拟小型端口边缘。 这允许提供程序通过绑定到多个物理网络适配器来支持 LBFO 解决方案。 这些物理网络适配器不受可扩展交换机驱动程序堆栈中运行的转发扩展管理。

    下图显示了 (Windows Server 2012 R2) 和更高版本的 NDIS 6.40 的 LBFO 团队配置示例。

    ![显示 ndis 6.40 的 lbfo 团队配置的流程图](images/vswitchteam3-ndis640.png)

    下图显示了 (Windows Server 2012) 的 NDIS 6.30 的 LBFO 团队配置示例。

    ![显示 ndis 6.30 的 lbfo 团队配置的流程图](images/vswitchteam3.png)

    **注意**  对于可扩展交换机扩展，基础 LBFO 团队将显示为绑定到外部网络适配器的单个虚拟网络适配器。

     

-   外部网络适配器可以绑定到 NDIS MUX 中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。

    在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。

    下图显示了 (Windows Server 2012 R2) 和更高版本的 NDIS 6.40 的可扩展交换机团队示例。

    ![显示 ndis 6.40 的可扩展交换机团队的流程图](images/vswitchteam-ndis640.png)

    下图显示了 (Windows Server 2012) 的 NDIS 6.30 的可扩展交换机团队示例。

    ![显示 ndis 6.30 的可扩展交换机团队的流程图](images/vswitchteam.png)

有关 MUX 驱动程序的详细信息，请参阅 [NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





