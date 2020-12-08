---
title: 用于 NDIS 状态指示的 hyper-v 可扩展交换机控制路径
description: NDIS 状态指示的 Hyper-V 可扩展交换机控制路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e040c87cec58c8d3598d0e7bf4131b894e0673a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814145"
---
# <a name="hyper-v-extensible-switch-control-path-for-ndis-status-indications"></a>NDIS 状态指示的 Hyper-V 可扩展交换机控制路径


本主题讨论底层物理适配器中 NDIS 状态指示的控制路径。 可以将一个或多个基础物理适配器与 Hyper-v 可扩展交换机外部网络适配器组合在一起。

例如，可扩展交换机外部网络适配器可以绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 中间驱动程序本身可以绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。 有关可扩展交换机团队的详细信息，请参阅 [物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展会公开给可扩展交换机团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 此类扩展称为 *组合提供程序*。 有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

**注意**  此类操作只能由转发扩展执行。 有关此类驱动程序的详细信息，请参阅 [转发扩展](forwarding-extensions.md)。

 

下图显示了 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的底层可扩展交换机团队颁发的用于 NDIS 状态指示的可扩展交换机控制路径。

![用于 ndis 6.40 的 vswitch 团队的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath2-ndis640.png)

下图显示了 ndis 6.30 (Windows Server 2012) 的底层可扩展交换机团队颁发的用于 NDIS 状态指示的可扩展交换机控制路径。

![用于 ndis 6.30 的 vswitch 团队的 ndis 状态指示的 vswitch 控制路径](images/vswitch-status-controlpath2.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。

 

可扩展交换机通过以下方式支持底层物理适配器或可扩展交换机团队的 NDIS 状态指示：

-   当 NDIS 状态指示到达可扩展交换机接口时，它会将指示封装到 [**ndis \_ 交换机 \_ NIC \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication) 结构内。 然后，可扩展交换机的微型端口边缘发出包含此结构的 [**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 指示。

    当转发扩展接收到此指示时，它可以重复指示以更改封装的数据。 这允许转发扩展更改所指示的基础可扩展交换机团队状态。

-   作为组合提供程序运行的转发扩展可以通过启动与卸载技术相关的 [**NDIS \_ 状态 \_ 交换机 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 指示，来参与适配器组的配置，以便进行硬件卸载。

    例如，提供程序可以使用封装的 [**NDIS \_ 状态 \_ 接收 \_ 筛选器 \_ 当前 \_ 功能**](./ndis-status-receive-filter-current-capabilities.md)指示来启动 [**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md)指示，以便在适配器组上修改虚拟机队列 (VMQ) 的卸载功能。

-   组合提供程序还可以启动 [**NDIS \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 指示来修改除可扩展交换机团队以外的其他网络适配器配置。

    例如，扩展可以启动 [**ndis \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) ，并使用封装的 [**NDIS \_ 状态 \_ 切换 \_ 端口 \_ 删除 \_ VF**](./ndis-status-switch-port-remove-vf.md) 指示。 此指示会删除虚拟机 (VM) 网络适配器与 PCI Express (PCIe) 虚函数 (VF) 之间的绑定。 VF 由支持单个根 i/o 虚拟化的基础物理网络适配器公开 (SR-IOV) 接口。

    删除此绑定之后，会通过可扩展交换机端口而不是直接在 VM 网络适配器和基础 SR-IOV 物理适配器的 VF 之间传输数据包。 这允许将可扩展交换机端口策略应用到通过可扩展交换机端口接收或发送的数据包。

**注意**  可扩展交换机扩展必须遵循相同的准则来筛选适用于所有 NDIS 筛选器驱动程序的 NDIS 状态指示。 有关详细信息，请参阅 [筛选模块状态指示](filter-module-status-indications.md)。

 

若要详细了解如何转发扩展可启动 [**ndis \_ 状态 \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 指示，请参阅 [从物理网络适配器管理 ndis 状态指示](managing-ndis-status-indications-from-physical-network-adapters.md)。

 

