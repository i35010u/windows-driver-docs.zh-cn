---
title: 处理 OID_NIC_SWITCH_CREATE_SWITCH 请求
description: 处理 OID_NIC_SWITCH_CREATE_SWITCH 请求
ms.assetid: 5C0BC300-8904-483A-A66B-8F5CFE0829B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d8a73062eeb7bf2f6fb0b85f0d626ff5fa6d59a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211065"
---
# <a name="handling-the-oid_nic_switch_create_switch-request"></a>处理 OID \_ NIC \_ 交换机 \_ 创建 \_ 切换请求


NDIS 发出对象标识符 (oid) 方法请求 [oid \_ NIC \_ 交换机 \_ CREATE \_ SWITCH](./oid-nic-switch-create-switch.md) 来执行以下操作：

-   在网络适配器上启用一个 NIC 交换机，该适配器是通过 PCI Express (PCIe 的微型端口驱动程序静态创建的，) 物理函数 (PF) 。 PF 是网络适配器的硬件组件，它支持 (SR-IOV) 的单个根 i/o 虚拟化。

    从上下文中将一个 NIC 交换机静态创建为对 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用。 驱动程序将分配资源并基于从注册表设置中读取的参数创建开关。

-   在网络适配器上动态创建 NIC 交换机。

    如果 PF 微型端口驱动程序不支持静态 NIC 交换机创建，微型端口驱动程序将根据在 OID 请求中指定的参数分配资源并创建开关。

当 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，PF 微型端口驱动程序会公布其 sr-iov 接口支持。 如果 PF 微型端口驱动程序支持 SR-IOV，NDIS 将从注册表中读取 NIC 交换机配置。 在 NDIS 发出 [oid \_ nic \_ 交换机 \_ CREATE \_ 切换](./oid-nic-switch-create-switch.md) 到 PF 微型端口驱动程序之前，ndis 会将 [**ndis \_ nic \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构的格式设置为以下方式：

-   NDIS 将 **SwitchType** 成员设置为 NIC 交换机的类型。

    从 Windows Server 2012 开始，Windows 仅支持交换机类型 **NdisNicSwitchTypeExternal**。 外部交换机指定连接到此类型的交换机 (VPorts) 的虚拟端口可以通过网络适配器上的物理端口访问外部网络。

    有关 NIC 交换机的详细信息，请参阅 [Sr-iov 体系结构](sr-iov-architecture.md)。

-   NDIS 将 **SwitchId** 成员设置为 NIC 交换机的标识符值。 交换机标识符是一个介于零和网络适配器所支持的开关数之间的整数。 NDIS \_ 默认 \_ 交换机 \_ ID 值指示默认 NIC 交换机。

    **注意**   从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的默认 NIC 交换机。

     

-   NDIS 设置 **NumVFs** 成员，该成员指定可在 NIC 交换机上分配的 (VFs) PCIe 虚拟函数的数目。

接收到 oid [ \_ NIC \_ 交换机 \_ CREATE \_ SWITCH](./oid-nic-switch-create-switch.md)的 oid 方法请求时，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态交换机创建和配置，它将在 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时创建 NIC 交换机。 当驱动程序处理此 OID 请求时，它必须验证 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构中的配置参数。 参数必须与驱动程序在调用 *MiniportInitializeEx*期间使用的参数相同。 如果不是这样，则驱动程序必须使 OID 请求失败。

    有关详细信息，请参阅 [创建 NIC 交换机的静态](static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态交换机创建和配置，则驱动程序必须验证 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构的配置值，并根据这些值创建 NIC 交换机。

    有关详细信息，请参阅 [动态创建 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

3.  PF 小型端口驱动程序必须为 NIC 交换机上的默认 VPort 分配必要的硬件和软件资源。

    **注意**   默认 VPort 始终通过 oid [ \_ nic \_ 交换机 \_ CREATE \_ 开关](./oid-nic-switch-create-switch.md)的 oid 请求创建，并通过 OID [ \_ nic \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md)的 oid 请求删除。 Oid [ \_ nic \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md) 和 [oid \_ nic \_ 交换机 \_ DELETE \_ VPORT](./oid-nic-switch-delete-vport.md) 的 Oid 请求用于在 NIC 交换机上创建和删除非默认 VPorts。

     

4.  支持动态交换机创建和配置的 PF 微型端口驱动程序必须通过调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)在交换机上启用 sr-iov 虚拟化。 此调用配置 **NumVFs** 成员，并且在适配器 PCI Express (PCIe) 配置空间的 Sr-iov 扩展功能结构中 **启用 "VF** "。

    有关 SR-IOV 配置空间的详细信息，请参阅 PCI-SIG [单根 I/o 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742) 规范。

    **注意**   如果 PF 微型端口驱动程序支持静态交换机创建，则在调用[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时，它将启用 sr-iov 虚拟化。

     

如果 PF 微型端口驱动程序已成功 completesthe oid \_ NIC 交换机 CREATE SWITCH 的 oid 方法请求 \_ \_ \_ ，则可以执行以下操作：

-   可以通过 oid [ \_ nic \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求，在 NIC 交换机上分配 VFs。

-   可以通过 oid [ \_ nic \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求在 NIC 交换机上创建非默认 VPorts。

    微型端口驱动程序负责管理其非默认 VPorts 池。 驱动程序通过[**NDIS \_ NIC \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构的**NumVPorts**成员指定其池中的非默认 VPorts 数。 驱动程序通过 oid [ \_ NIC \_ 交换机 \_ 枚举 \_ 开关](./oid-nic-switch-enum-switches.md)的 oid 查询请求返回此结构。

    **注意**   网络适配器必须始终从其池中为 PF 创建默认 VPort。

     

 

