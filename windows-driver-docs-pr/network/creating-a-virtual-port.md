---
title: 创建虚拟端口
description: 创建虚拟端口
ms.assetid: 6102576D-3236-4FDD-8963-83A9E90FF7F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1b27a68a95763d43226600c5fb42d2ebd9291fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540677"
---
# <a name="creating-a-virtual-port"></a>创建虚拟端口


虚拟端口 (VPort) 是一个数据对象，表示支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的 NIC 交换机上的内部端口。 每个 NIC 交换机提供网络连接的以下端口：

-   连接到外部物理网络的一个外部物理端口。

-   一个或多个内部 VPorts 连接到的 PCI Express (PCIe) 物理函数 (PF) 或虚函数 (VFs)。

    PF 附加到 HYPER-V 父分区，并公开为该分区中运行管理操作系统中的虚拟网络适配器。

    取景器附加到 HYPER-V 子分区，并公开为该分区中运行来宾操作系统中的虚拟网络适配器。

有两种类型的 VPorts:

<a href="" id="default-vport"></a>默认 VPort  
默认值 VPort 提供网络连接到在管理操作系统中运行的网络组件。 默认 VPort 具有标识符的 NDIS\_默认\_VPORT\_id。

该驱动程序时 PF 微型端口驱动程序创建和配置默认 NIC 开关时，隐式创建默认 VPort 并将其附加到 PF. 默认 VPort 无法附加到 VF。

默认值 VPort 始终处于激活状态，无法显式删除。 仅当删除 NIC 切换的默认值时，PF 微型端口驱动程序隐式删除默认 VPort。

有关如何创建一个 NIC 开关和默认 VPort 交换机上的详细信息，请参阅[创建 NIC 切换](creating-a-nic-switch.md)。

<a href="" id="nondefault-vport"></a>非默认 VPort  
创建 NIC 开关时，不会隐式创建非默认 VPorts。 基础驱动程序，如虚拟化堆栈中，通过发出 OID 方法请求的显式创建这些端口[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)。 非默认 VPorts 到 PF 或 VF 可能附加，并且只能在创建 NIC 开关后创建。

非默认附加到 VF VPort 提供网络连接到在来宾操作系统中运行的网络组件。 创建并附加到 VF 后，非默认 VPort 处于激活状态。

非默认附加到 PF VPort 提供额外的网络卸载功能在管理操作系统中运行的网络组件。 例如，非默认 VPorts PF 上的无法用于提供卸载功能类似于虚拟机队列 (VMQ) 接口。

**请注意**创建 NIC 开关后，可以仅创建非默认 VPorts。



基础驱动程序发出的一个对象标识符 (OID) 方法请求[OID\_NIC\_切换\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)指定 NIC 交换机上创建非默认 VPort。 此 OID 请求还将创建的 VPort 附加到网络适配器的 PF 或以前分配的取景器。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[**NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构。 从成功返回后[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)请求， **VPortId**隶属**NDIS\_NIC\_切换\_VPORT\_参数**结构都有在 NIC 交换机上 VPorts 中是唯一一个 VPort 标识符。

基础驱动程序初始化[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)的配置信息的结构有关非默认 VPort 创建。 配置信息包括向其附加 VPort 非默认和数量的队列对的非默认 VPort PCIe 函数。

当它初始化[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构，基础驱动程序必须执行以下操作：

-   **SwitchId**成员必须设置为先前通过 OID 方法请求的网络适配器创建一个 NIC 开关的标识符[OID\_NIC\_切换\_创建\_交换机](https://msdn.microsoft.com/library/windows/hardware/hh451815)。

    **请注意**从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 交换机*。 在创建非默认 VPort，必须设置基础驱动程序**SwitchId**成员添加到 NDIS\_默认\_交换机\_ID 标识符。



-   **VPortId**成员必须设置为 NDIS\_默认\_VPORT\_id。

-   **AttachedFunctionId**成员必须设置为取景器或非默认 VPort 是要附加的 PF 的标识符。

    值为 NDIS\_PF\_函数\_ID 指定 PF. 否则，值必须设置为取景器之前通过 OID 方法请求的分配的资源的标识符[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。

    **请注意**VPort 已创建非默认后无法更改到 VF 或 PF 的非默认 VPort 附件。



基础驱动程序还可以指定分配给 VPort 队列对的数目。 队列对是传输和接收队列分配给 VPort 的网络适配器上。 如果网络适配器支持非对称队列对的非默认 VPorts，基础驱动程序可能会为驱动程序创建每个 VPort 指定不同数量的队列对。 有关详细信息，请参阅[对称和非对称队列分配对](symmetric-and-asymmetric-assignment-of-queue-pairs.md)。

过量的驱动程序调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)颁发[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)对基础 PF 微型端口驱动程序的请求。 NDIS OID 方法将请求转发到微型端口驱动程序之前，请执行以下操作：

1.  NDIS 验证中的参数[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)结构。 如果参数在错误，NDIS OID 方法请求失败，且不将请求传递到 PF 微型端口驱动程序。

2.  NDIS 将非默认 VPort 范围内的标识符分配从一个到 (**NumVPorts**– 1)，其中**NumVPorts**是 VPorts 微型端口驱动程序已配置网络适配器的数字。 该驱动程序指定中的此编号**NumVPorts**的成员[ **NDIS\_NIC\_开关\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh451582)结构。 驱动程序将返回通过 OID 查询请求的此结构[OID\_NIC\_交换机\_枚举\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451819)。

    **请注意**VPort 标识符的 NDIS\_默认\_VPORT\_ID 保留为默认值附加到默认 NIC 交换机上 PF VPort。




分配的 VPort 标识符唯一标识非默认 VPort NIC 交换机的网络适配器上。


3.  NDIS 集**VPortId**成员的 NDIS\_NIC\_交换机\_VPORT\_具有分配的 VPort 标识符的参数结构。

PF 微型端口驱动程序发出 OID 请求，该驱动程序会分配与指定非默认 VPort 关联的硬件和软件资源。 通过返回 NDIS 组件时 PF 微型端口驱动程序的所有资源已成功分配后，已成功完成 OID\_状态\_从成功[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416).

如果[OID\_NIC\_交换机\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)请求已成功完成后，PF 微型端口驱动程序和基础驱动程序必须保留**VPortId** VPort 连续的操作的非默认值。 **VPortId**进行这些操作时使用值：

-   使用 NDIS 和基础驱动程序**VPortId**值以标识非默认中连续 OID VPort 请求与此 VPort 相关如[OID\_NIC\_开关\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)并[OID\_NIC\_开关\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)。

-   在发送操作期间指定 NDIS **VPortId**值以标识从其发送数据包 VPort。 带外 (OOB) 中指定此值[ **NDIS\_NET\_缓冲区\_列表\_筛选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566567)的数据[NET\_缓冲区\_列表](net-buffer-list-structure.md)结构。

-   在接收操作，PF 微型端口驱动程序指定**VPortId**数据包将转发到的值。 此值还指定在 OOB [ **NDIS\_NET\_缓冲区\_列表\_筛选\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff566567) 数据[NET\_缓冲区\_列表](net-buffer-list-structure.md)结构。

以下各点适用于非默认 VPorts 创建：

-   筛选器的接收程序媒体访问控制 (MAC) 并创建它后 VPort 上配置虚拟 LAN (VLAN) 标识符。 动态过量驱动程序中设置这些筛选器接收通过发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。 接收筛选器还可以从一个到另一个通过 OID VPort 设置的请求移[OID\_接收\_筛选器\_移动\_筛选器](https://msdn.microsoft.com/library/windows/hardware/hh451845)。

-   非默认 VPort 附加到 VF 处于激活状态，在创建时。 不能停用 VPort，如果它已附加到 VF。

    在创建时，非默认 VPort 附加到 PF 是处于停用状态。 基础驱动程序，如 HYPER-V 可扩展交换机模块，显式激活后已成功创建 VPort VPort 附加到 PF 非默认。 这是通过发出的 OID 方法请求[OID\_NIC\_交换机\_VPORT\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451825)到 PF 微型端口驱动程序。

    当基础驱动程序将发出此 OID 请求时，会传递[ **NDIS\_NIC\_交换机\_VPORT\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451597)具有结构**VPortState**成员设置为**NdisNicSwitchVPortStateActivated**。

    在非默认 VPort 处于激活状态之后, PF 微型端口驱动程序可以共享的内存为分配 VPort 通过调用[ **NdisAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff561616)。 该驱动程序必须设置**VPortId**中的成员[ **NDIS\_共享\_内存\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567303) VPort 的结构标识符值。

**请注意**时非默认 VPort 处于激活状态，它才可设置为已停用状态通过 OID 集请求的删除时[OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818).











