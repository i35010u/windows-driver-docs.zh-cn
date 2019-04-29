---
title: 虚拟端口 (VPort)
description: 虚拟端口 (VPort)
ms.assetid: FCE0B5F5-5E2E-493A-BE25-57FB2C8B0389
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f1875343a6de5ef827f13f3b2b699618deda236
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366648"
---
# <a name="virtual-ports-vports"></a>虚拟端口 (VPort)


虚拟端口 (VPort) 是数据对象，表示支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的 NIC 交换机上的内部端口。 每个 NIC 交换机提供网络连接的以下端口：

-   连接到外部物理网络的一个外部物理端口。

-   一个或多个内部 VPorts 连接到的 PCI Express 物理函数 (PF) 或虚函数 (VFs)。

    PF 附加到 HYPER-V 父分区，并公开为该分区中运行管理操作系统中的虚拟网络适配器。

    取景器附加到 HYPER-V 子分区，并公开为该分区中运行来宾操作系统中的虚拟网络适配器。

NIC 到一个或多个 VPorts 切换从物理端口的桥网络流量。 这提供了对基础物理网络接口的虚拟化的访问。

每个 VPort 都有一个唯一标识符 (*VPortId*) 这是唯一的网络适配器上的 NIC 开关。 默认 VPort 始终默认 NIC 交换机上存在，并且永远不会被删除。 默认值 VPort 具有 NDIS VPortId\_默认\_VPORT\_id。

当 PF 微型端口驱动程序处理的对象标识符 (OID) 方法请求[OID\_NIC\_切换\_创建\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451815)，它会创建 NIC 开关和默认值为 VPort该开关。 默认值 VPort 始终附加到 PF，并始终处于运行状态。

通过 OID 方法请求的创建非默认 VPorts [OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。 只有一个非默认 VPort 可以附加到 VF。 附加完成后，默认值为的操作状态。 一个或多个非默认 VPorts 还可以创建并附加到 PF. 这些 VPorts 不再运行时创建，并且可能会变得通过 OID 集请求的操作[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)。

**请注意**后 VPort 开始运行，它可以仅会变得不再运行时通过的 OID 请求删除[OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818).



每个 VPort 具有一个或多个硬件队列对关联的接收和传输数据包。 默认情况下 VPort 情况下，网络适配器上的默认队列对保留供使用。 队列对的非默认分配和分配时通过创建 VPort VPorts [OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)请求。

创建和配置通过 OID 方法请求的非默认 VPorts [OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。 通过 OID 集请求的重新配置的默认 VPort 和非默认 VPorts [OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)。 每个 OID 请求包含[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构，它指定下面的配置参数：

-   VPort 附加到 PCIe 函数。

    每个 VPort 可以或者附加到 PF 或 VF 在任何时间。 创建并附加到 PCIe 函数 VPort 后，附件不能动态更改为另一个 PCIe 函数。

    **请注意**VPort 始终附加到网络适配器上 PF 默认值。




开始在 Windows Server 2012 中，只有一个非默认的 NDIS 6.30 VPort 可以附加到 VF。 但是，可以将多个非默认 VPorts 默认 VPort 以及附加到 PF.


-   分配给 VPort 的硬件队列对的数目。

    每个 VPort 具有一组可供它的硬件队列对。 每个队列对由单独传输和接收的网络适配器上的队列。

    队列对是有限的网络适配器上的资源。 创建 NIC 开关时指定的队列对保留以供默认和非默认 VPorts 总数。 这允许分配给默认 VPort 不同于非默认 VPorts 的队列对的数目。

    每个非默认 VPort 可以配置为具有不同数目的队列对。 这称为*非对称分配*队列对。 如果 NIC 不允许此类的非对称分配，每个非默认 VPort 被配置为具有同等数量的队列对。 这称为*对称分配*队列对。 有关详细信息，请参阅[对称和非对称队列分配对](symmetric-and-asymmetric-assignment-of-queue-pairs.md)。

    **请注意**PF 微型端口驱动程序报告它是否支持非对称分配的队列对期间[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。 有关详细信息，请参阅[初始化 PF 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。




分配给每个 VPort 队列对的数目不会动态更改。 创建 VPort 后无法更改分配给 VPort 队列对的数目。

**请注意**分配给 VPorts 可用于非默认的一个或多个队列对接收方缩放 (RSS) 通过在来宾操作系统中运行的 VF 微型端口驱动程序。




-   有关 VPort 中断裁决参数。

    可以为不同 VPorts 指定不同的中断裁决类型。 这样，虚拟化堆栈来控制生成的特定 VPort 中断的数量。

除了配置过量驱动程序的参数，可以配置接收筛选器的每个 VPort 通过发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795). NIC 开关执行指定接收 VPort 基础上筛选。

接收 VPorts 包括数据包筛选条件，例如媒体访问控制 (MAC) 地址和虚拟 LAN (VLAN) 标识符的列表筛选器参数。 对 MAC 地址和 VLAN 标识符筛选器中指定始终一起[ **NDIS\_接收\_筛选器\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567181) 与相关联[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)请求。 NIC 交换机必须筛选到交换机的传入数据包的目标 MAC 地址和 VLAN 标识符与 VPort 设置任何接收筛选条件相匹配。 NIC 交换机筛选从任一另一个 VPort 或从外部物理端口接收的数据包。 如果数据包与筛选器相匹配，NIC 交换机必须将其转发到 VPort。

可能会对 VPort 设置多个 MAC 地址和 VLAN 标识符对。 如果仅设置 MAC 地址，接收筛选器指定 VPort 应接收数据包符合以下条件：

-   数据包的目标 MAC 地址与筛选器的 MAC 地址相匹配。

-   数据包的 VLAN 标记或 （如果 VLAN 标记为存在） 的零为 VLAN 标识符。

通过 OID 的集请求删除非默认 VPorts [OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。 默认值通过 OID 集请求的删除 NIC 开关时，仅删除 VPort [OID\_NIC\_切换\_删除\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451817)。









