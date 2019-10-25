---
title: 确定 NIC 交换机功能
description: 确定 NIC 交换机功能
ms.assetid: 5E627E52-2D47-4EA0-80D9-6979891CCE96
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798279568e9a5b5629eb075164bf8a6116229464
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834914"
---
# <a name="determining-nic-switch-capabilities"></a>确定 NIC 交换机功能


本主题介绍 NDIS 和过量驱动程序如何确定支持单个根 i/o 虚拟化（SR-IOV）的网络适配器的 NIC 交换机功能。 本主题包含下列信息：

[在*MiniportInitializeEx*期间报告 NIC 交换机功能](#reporting-nic-switch-capabilities-during-miniportinitializeex)

[查询过量驱动程序的 NIC 交换机功能](#querying-nic-switch-capabilities-by-overlying-drivers)

**请注意**  仅适用于 sr-iov 网络适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序可以报告 NIC 交换机功能。 PCIe 虚拟功能（VFs）的微型端口驱动程序不得报告 SR-IOV 适配器的 NIC 交换机功能。

 

有关 NIC 交换机的详细信息，请参阅[Nic 交换机](nic-switches.md)。

## <a name="reporting-nic-switch-capabilities-during-miniportinitializeex"></a>在*MiniportInitializeEx*期间报告 NIC 交换机功能


当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序提供以下 NIC 交换机功能：

-   网络适配器可支持的 NIC 交换机的完整硬件功能集。

    **注意**  从 NDIS 6.30 开始，网络适配器上只创建了一个 NIC 交换机。 此开关称为 "*默认 NIC 交换机*"。     

-   当前已在网络适配器上启用的 NIC 交换机功能。

微型端口驱动程序通过[**NDIS\_nic\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构，通过以下方式初始化基础网络适配器的 nic 交换机硬件功能：

1.  微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_默认值。

    从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 NDIS\_NIC\_交换机\_功能\_修订版\_2，并将**Size**成员设置为 ndis\_SIZEOF\_\_2\_交换机\_功能\_修订版本。

2.  微型端口驱动程序在[**NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)的**NicSwitchCapabilities**成员中设置相应的标记\_将\_功能结构转换为 SR-IOV 网络适配器的 NIC 交换机功能。 例如，如果 NIC 交换机支持每个虚拟端口上的中断裁决，微型端口驱动程序会将 NDIS\_NIC\_交换机\_CAP\_每个\_VPORT\_中断\_仲裁\_支持的标志。VPort）在交换机上创建的。

3.  微型端口驱动程序将[**NDIS\_\_nic**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)的其他成员设置为 sr-iov 网络适配器的 nic 交换机功能的值范围\_功能结构。 例如，微型端口驱动程序将**MaxNumVFs**和**MaxNumVPorts**成员设置为适配器可支持的最大 VFs 和 VPorts 数。

    **请注意**  根据网络适配器上的可用硬件资源，微型端口驱动程序可以将**MaxNumVFs**成员设置为小于其 **\*NumVFs**关键字的值。 有关此关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

     

当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序会按照以下步骤注册网络适配器的 NIC 交换机功能：

1.  微型端口驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

    微型端口驱动程序将**HardwareNicSwitchCapabilities**成员设置为指向先前初始化的[**NDIS\_NIC 的指针\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

    如果 **\*SRIOV** INF 关键字的注册表设置值为1，则当前启用了 NIC 交换机创建和配置网络适配器。 微型端口驱动程序将**CurrentNicSwitchCapabilities**成员设置为指向同一[**NDIS\_NIC 的指针\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

    如果 **\*SRIOV** INF 关键字的注册表设置值为零，则当前没有为网络适配器启用 NIC 交换机创建和配置。 微型端口驱动程序必须将**CurrentNicSwitchCapabilities**成员设置为 NULL。

    有关 **\*SRIOV** INF 关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

2.  驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="creating-a-nic-switch-without-sr-iov"></a>不用 SR-IOV 创建 NIC 交换机

在 NDIS 6.60 和更高版本中，小型端口驱动程序必须遵守 NIC 交换机的共存要求，以及未启用 SR-IOV 时的 VMQ 功能。 启用 SR-IOV 后，微型端口驱动程序应遵循上一节中的现有要求。

- 微型端口驱动程序公布 NIC 交换机和 VMQ 功能。
- NIC 无需重新启动即可在 NIC 交换机和 VMQ 模式之间切换。
    - NIC 最初启动时，可以处于任一模式（创建 NIC 交换机或创建 VMQ 队列）。
        - 如果创建了 NIC 交换机，则微型端口会失败任何后续的 VMQ 队列分配回调。
        - 如果首先创建 VMQ 队列，微型端口驱动程序会成功执行 VMQ 队列分配，并使任何 NIC 交换机分配调用失败。
    - 如果删除了 NIC 交换机，或者删除了所有 VMQ 队列，则微型端口驱动程序将返回到初始状态，并准备好进入这两种模式。

若要播发可以在不使用 SR-IOV 的情况下创建 NIC 交换机，微型端口驱动程序在 NDIS\_NIC 的**NicSwitchCapabilities**成员中设置**NDIS_NIC_SWITCH_CAPS_NIC_SWITCH_WITHOUT_IOV_SUPPORTED**标志[ **\_切换\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

## <a name="querying-nic-switch-capabilities-by-overlying-drivers"></a>查询过量驱动程序的 NIC 交换机功能


NDIS 通过以下方式将网络适配器的当前启用的 NIC 交换机功能传递到绑定到网络适配器的过量驱动程序：

-   当 NDIS 调用过量筛选器驱动程序的[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数时，Ndis 通过*AttachParameters*参数传递网络适配器的 NIC 交换机功能。 此参数包含指向[**NDIS\_筛选器的指针\_ATTACH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 此结构的**NicSwitchCapabilities**成员包含指向[**NDIS\_NIC 的指针\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

-   当 NDIS 调用过量协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 通过*BindParameters*参数传递网络适配器的 NIC 交换机功能。 此参数包含指向[**NDIS\_筛选器的指针\_ATTACH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 此结构的**NicSwitchCapabilities**成员包含指向[**NDIS\_NIC 的指针\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构。

在处理\_OID 的对象标识符（OID）查询请求时，NDIS 还会返回[**ndis\_nic\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构\_[交换机\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-hardware-capabilities)和[OID\_NIC\_交换机\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-current-capabilities)由过量协议或筛选器驱动程序颁发的当前\_功能。

 

 





