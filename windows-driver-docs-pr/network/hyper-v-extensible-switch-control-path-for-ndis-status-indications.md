---
title: 用于 NDIS 状态指示的 hyper-v 可扩展交换机控制路径
description: NDIS 状态指示的 Hyper-V 可扩展交换机控制路径
ms.assetid: D52FAC95-64EC-4A99-807A-B39DB136D8F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49cc4854af6c6748337c137093fc02a654176037
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823928"
---
# <a name="hyper-v-extensible-switch-control-path-for-ndis-status-indications"></a>NDIS 状态指示的 Hyper-V 可扩展交换机控制路径


本主题讨论底层物理适配器中 NDIS 状态指示的控制路径。 可以将一个或多个基础物理适配器与 Hyper-v 可扩展交换机外部网络适配器组合在一起。

例如，可扩展交换机外部网络适配器可以绑定到 NDIS 多路复用器（MUX）中间驱动程序的虚拟微型端口边缘。 MUX 中间驱动程序本身可以绑定到主机上一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队的详细信息，请参阅[物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展会公开给可扩展交换机团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为团队提供负载平衡故障转移（LBFO）解决方案的支持。 此类扩展称为*组合提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

**请注意**，此排序  操作只能由转发扩展执行。 有关此类驱动程序的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

 

下图显示了 NDIS 6.40 （Windows Server 2012 R2）和更高版本的基础可扩展交换机团队颁发的 NDIS 状态指示的可扩展交换机控制路径。

![用于 ndis 6.40 的 vswitch 团队的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath2-ndis640.png)

下图显示了 NDIS 6.30 的底层可扩展交换机团队颁发的 NDIS 状态指示的可扩展交换机控制路径（Windows Server 2012）。

![用于 ndis 6.30 的 vswitch 团队的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath2.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为*可扩展交换机扩展*，驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。

 

可扩展交换机通过以下方式支持底层物理适配器或可扩展交换机团队的 NDIS 状态指示：

-   当 NDIS 状态指示到达可扩展交换机接口时，它会将指示封装在[**ndis\_交换机\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构。 然后，可扩展交换机的微型端口边缘[ **\_交换机\_NIC\_状态指示\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)包含此结构的状态。

    当转发扩展接收到此指示时，它可以重复指示以更改封装的数据。 这允许转发扩展更改所指示的基础可扩展交换机团队状态。

-   作为组合提供程序运行的转发扩展可以通过启动[**NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示（与卸载技术相关）来参与适配器组的配置。

    例如，提供程序可以启动[**NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示与封装的[**NDIS\_状态\_接收\_筛选器\_当前\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-filter-current-capabilities)指示来修改适配器组上的虚拟机队列（VMQ）的卸载功能。

-   组合提供程序还可以启动[**NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示来修改可扩展交换机团队以外的其他网络适配器配置。

    例如，扩展可以[ **\_状态启动 NDIS 状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)与封装的[**NDIS\_状态\_交换机\_端口\_删除\_VF**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-port-remove-vf)指示。 此指示删除虚拟机（VM）网络适配器与 PCI Express （PCIe）虚拟功能（VF）之间的绑定。 VF 由支持单根 i/o 虚拟化（SR-IOV）接口的基础物理网络适配器公开。

    删除此绑定之后，会通过可扩展交换机端口而不是直接在 VM 网络适配器和基础 SR-IOV 物理适配器的 VF 之间传输数据包。 这允许将可扩展交换机端口策略应用到通过可扩展交换机端口接收或发送的数据包。

**请注意**  可扩展交换机扩展必须遵循相同的准则来筛选适用于所有 NDIS 筛选器驱动程序的 ndis 状态指示。 有关详细信息，请参阅[筛选模块状态指示](filter-module-status-indications.md)。

 

若要详细了解转发扩展如何启动[**NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示，请参阅[从物理网络适配器管理 ndis 状态指示](managing-ndis-status-indications-from-physical-network-adapters.md)。

 

 





