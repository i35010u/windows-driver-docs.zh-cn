---
title: 类型的物理网络适配器配置
description: 类型的物理网络适配器配置
ms.assetid: 83F71AF7-A807-4F81-A0B3-1777135AAE39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b33f31989c5df18e65ec11a09981db1acf11e29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521866"
---
# <a name="types-of-physical-network-adapter-configurations"></a>类型的物理网络适配器配置


HYPER-V 可扩展交换机体系结构支持与单个外部网络适配器连接到基础物理介质的访问。 外部网络适配器可以绑定到以下物理网络适配器配置之一：

-   外部网络适配器可以绑定到单一的基础物理网络适配器。 在此配置中，可扩展交换机扩展公开到并管理在主机上只有一个基础的网络适配器。

    下图显示了外部网络适配器绑定到单一物理网络适配器的 NDIS 6.40 (Windows Server 2012 R2) 及更高版本的可扩展交换机配置。

    ![vswitch 配置与外部网络适配器绑定到单一物理网络适配器的 ndis 6.40 及更高版本](images/vswitchsingle-ndis640.png)

    下图显示了在其中的外部网络适配器绑定到单一物理网络适配器的 NDIS 6.30 (Windows Server 2012) 的可扩展交换机配置。

    ![与外部网络适配器绑定到单个物理网络适配器的 ndis 6.30 vswitch 配置](images/vswitchsingle.png)

-   外部网络适配器可以绑定到负载平衡故障转移 (LBFO) 提供程序的虚拟微型端口边缘。 这是 NDIS 多路复用器 (MUX) 驱动程序，它可能会在主机上绑定到团队的一个或多个物理网络上进行分层的 NDIS 筛选器驱动程序。 此配置称为*LBFO 团队*。

    在此配置中，可扩展交换机扩展公开到仅基础虚拟微型端口边缘为网络适配器。 这允许提供程序支持通过绑定到多个物理网络适配器 LBFO 解决方案。 这些物理网络适配器不受在可扩展交换机驱动程序堆栈中运行的转发扩展。

    下图显示了 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的 LBFO 团队配置的示例。

    ![显示 ndis 6.40 lbfo 团队配置流程图](images/vswitchteam3-ndis640.png)

    下图显示 LBFO 团队配置的一个示例为 NDIS 6.30 (Windows Server 2012)。

    ![显示 ndis 6.30 lbfo 团队配置流程图](images/vswitchteam3.png)

    **请注意**  可扩展交换机扩展的基础 LBFO 团队显示为绑定到外部网络适配器的单个虚拟网络适配器。

     

-   外部网络适配器可以绑定到 NDIS MUX 中间驱动程序的虚拟微型端口边缘。 MUX 驱动程序绑定到一个或多个物理网络的团队在主机上。 此配置称为*可扩展交换机团队*。

    在此配置中，向团队中每个网络适配器公开可扩展交换机扩展。 这允许要管理的配置和使用的团队中的单个网络适配器的扩展。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。

    下图显示了一个可扩展交换机团队 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的示例。

    ![显示可扩展流程图切换 ndis 6.40 团队](images/vswitchteam-ndis640.png)

    下图显示的 NDIS 6.30 (Windows Server 2012) 的可扩展交换机团队的示例。

    ![显示可扩展流程图切换 ndis 6.30 团队](images/vswitchteam.png)

MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





