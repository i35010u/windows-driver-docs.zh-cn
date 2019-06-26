---
title: NDIS 指示状态的 HYPER-V 可扩展交换机控制路径
description: NDIS 状态指示的 Hyper-V 可扩展交换机控制路径
ms.assetid: D52FAC95-64EC-4A99-807A-B39DB136D8F9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae452a4338684975a2d4487066292c158f45e02d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383702"
---
# <a name="hyper-v-extensible-switch-control-path-for-ndis-status-indications"></a>NDIS 状态指示的 Hyper-V 可扩展交换机控制路径


本主题讨论从基础物理适配器的 NDIS 状态指示在之间移动的控制路径。 一个或多个基础物理适配器可以使用的 HYPER-V 可扩展交换机外部网络适配器成组。

例如，可扩展交换机外部网络适配器可以绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 在主机上，MUX 中间驱动程序本身可以绑定到一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展公开到可扩展交换机团队中每个网络适配器。 这样，转发扩展中要管理的配置和使用的团队中的单个网络适配器的可扩展交换机驱动程序堆栈。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 此类扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

**请注意**  这类操作只能由转发扩展。 有关此类型的驱动程序的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

 

下图显示了 NDIS 状态指示颁发的底层的可扩展交换机团队 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机控制路径。

![ndis 状态指示从 ndis 6.40 vswitch 团队的 vswitch 控制路径](images/vswitch-status-controlpath2-ndis640.png)

下图显示了 NDIS 状态指示在 NDIS 6.30 (Windows Server 2012) 发出由底层的可扩展交换机团队的可扩展交换机控制路径。

![ndis 状态指示从 ndis 6.30 vswitch 团队的 vswitch 控制路径](images/vswitch-status-controlpath2.png)

**请注意**  可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*.

 

可扩展交换机支持的基础物理适配器或可扩展交换机团队从 NDIS 状态指示以下方面：

-   当在可扩展交换机接口到达 NDIS 状态指示时，它封装在指示[ **NDIS\_切换\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构。 然后，可扩展交换机问题的微型端口边缘[ **NDIS\_状态\_切换\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示包含此结构。

    当转发扩展收到这种指示时，它可以重复的指示来更改封装的数据。 这样，转发扩展，若要更改所指示的状态或底层的可扩展交换机团队的能力。

-   通过启动将会像组合的提供程序可以参与的硬件的适配器组配置的转发扩展，卸载[ **NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)的卸载技术与相关的迹象。

    例如，可以启动该提供程序[ **NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指示与封装[ **NDIS\_状态\_接收\_筛选器\_当前\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-receive-filter-current-capabilities)表示要修改的卸载功能有关适配器组上的虚拟机队列 (VMQ)。

-   组合提供程序还可启动[ **NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)表示要修改其他网络适配器可扩展交换机团队以外的配置。

    例如，可以启动扩展[ **NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)与封装[ **NDIS\_状态\_交换机\_端口\_删除\_VF** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-port-remove-vf)指示。 此指示删除虚拟机 (VM) 网络适配器和 PCI Express (PCIe) 的虚拟函数 (VF) 之间的绑定。 VF 公开基础物理网络适配器支持的单个根 I/O 虚拟化 (SR-IOV) 接口。

    删除此绑定后，数据包会通过可扩展的交换机端口而不是直接在 VM 网络适配器和基础 SR-IOV 物理适配器的 VF 之间传递。 这样，可扩展交换机端口策略应用于接收或通过可扩展交换机端口发送的数据包。

**请注意**  可扩展交换机扩展必须遵循用于筛选适用于所有 NDIS 筛选器驱动程序的 NDIS 状态指示的相同准则。 有关详细信息，请参阅[筛选器模块状态指示](filter-module-status-indications.md)。

 

有关如何启动转发扩展的详细信息[ **NDIS\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)指标，请参阅[管理从物理网络适配器的 NDIS 状态指示](managing-ndis-status-indications-from-physical-network-adapters.md)。

 

 





