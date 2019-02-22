---
title: 确定 NIC 交换机功能
description: 确定 NIC 交换机功能
ms.assetid: 5E627E52-2D47-4EA0-80D9-6979891CCE96
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990104d4b1d07ef6bdb8e1f4b3933c4316457bee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541270"
---
# <a name="determining-nic-switch-capabilities"></a>确定 NIC 交换机功能


本主题介绍 NDIS 和基础驱动程序如何确定 NIC 切换支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器的功能。 本主题包含下列信息：

[报告期间的 NIC 交换机功能*MiniportInitializeEx*](#report)

[查询 NIC 交换机功能的基础驱动程序](#query)

**请注意**  仅微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 网络适配器可以报告 NIC 交换机功能。 PCIe 虚函数 (VFs) 的微型端口驱动程序必须报告 NIC 切换 SR-IOV 适配器功能。

 

有关 NIC 开关的详细信息，请参阅[NIC 开关](nic-switches.md)。

## <a name="reporting-nic-switch-capabilities-during-miniportinitializeex"></a>报告期间的 NIC 交换机功能*MiniportInitializeEx*


当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序提供了以下 NIC 切换功能：

-   一组完整的网络适配器可以支持的 NIC 交换机的硬件功能。

    **请注意**  从 NDIS 6.30 开始，只有一个 NIC 创建交换机上的网络适配器。 此交换机被称为*默认 NIC 交换机*。

     

-   NIC 切换当前网络适配器已启用的功能。

微型端口驱动程序报告的 NIC 交换机硬件功能的基础网络适配器通过[ **NDIS\_NIC\_切换\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)按以下方式初始化结构：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。

    从开始 NDIS 6.30，微型端口驱动程序设置**修订**的成员**标头**到 NDIS\_NIC\_开关\_功能\_修订版本\_2，**大小**成员添加到 NDIS\_SIZEOF\_NIC\_开关\_功能\_修订\_2。

2.  微型端口驱动程序设置相应的标记**NicSwitchCapabilities**的成员[ **NDIS\_NIC\_开关\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583) SR-IOV 网络适配器的 NIC 交换机功能的结构。 例如，微型端口驱动程序设置 NDIS\_NIC\_交换机\_CAP\_每\_VPORT\_中断\_审查\_支持标志，如果 NIC交换机支持在交换机创建每个虚拟端口 (VPort) 上中断裁决。

3.  微型端口驱动程序设置的其他成员[ **NDIS\_NIC\_切换\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构到 NIC 的交换机功能的值的范围SR-IOV 网络适配器。 例如，微型端口驱动程序设置**MaxNumVFs**并**MaxNumVPorts** VFs 和 VPorts 的适配器可以支持的最大数目的成员。

    **请注意**  微型端口驱动程序可以根据网络适配器上的可用硬件资源，设置**MaxNumVFs**成员添加到的值不会早于其 **\*NumVFs**关键字。 有关此关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

     

当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序注册的网络适配器的 NIC 交换机功能通过执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

    微型端口驱动程序集**HardwareNicSwitchCapabilities**指向以前初始化的指针到成员[ **NDIS\_NIC\_开关\_功能** ](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。

    如果的注册表设置 **\*SRIOV** INF 关键字的一个值，则网络适配器当前已启用 NIC 交换机创建和配置。 微型端口驱动程序集**CurrentNicSwitchCapabilities**指向相同的指针到成员[ **NDIS\_NIC\_开关\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。

    如果的注册表设置 **\*SRIOV** INF 关键字的值为零、 网络适配器当前未启用 NIC 交换机创建和配置。 微型端口驱动程序必须设置**CurrentNicSwitchCapabilities**为 NULL 的成员。

    有关详细信息 **\*SRIOV** INF 关键字，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

2.  驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置*MiniportAttributes*参数指向的指针[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-nic-switch-capabilities-by-overlying-drivers"></a>查询 NIC 交换机功能的基础驱动程序


NDIS 传递网络适配器的当前已启用 NIC 交换机功能到过量按以下方式绑定到的网络适配器的驱动程序：

-   当 NDIS 调用过量的筛选器驱动程序的[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数，NDIS 传递网络适配器的 NIC 交换机功能通过*AttachParameters*参数。 此参数包含一个指向[ **NDIS\_筛选器\_附加\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构。 **NicSwitchCapabilities**此结构的成员包含一个指向[ **NDIS\_NIC\_开关\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。

-   当 NDIS 调用基础协议驱动[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数，NDIS 传递网络适配器的 NIC 交换机功能通过*BindParameters*参数。 此参数包含一个指向[ **NDIS\_筛选器\_附加\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构。 **NicSwitchCapabilities**此结构的成员包含一个指向[ **NDIS\_NIC\_开关\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构。

NDIS 也会返回[ **NDIS\_NIC\_交换机\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566583)结构，它处理的对象标识符 (OID) 查询请求时[OID\_NIC\_交换机\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569761)并[OID\_NIC\_交换机\_当前\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569760)，颁发的过量协议或筛选器驱动程序。

 

 





