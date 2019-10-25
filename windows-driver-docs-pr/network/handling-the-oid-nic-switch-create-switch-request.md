---
title: 处理 OID_NIC_SWITCH_CREATE_SWITCH 请求
description: 处理 OID_NIC_SWITCH_CREATE_SWITCH 请求
ms.assetid: 5C0BC300-8904-483A-A66B-8F5CFE0829B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cfb723ba54a3fe109b1a2c45ab4c0072834f8ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842555"
---
# <a name="handling-the-oid_nic_switch_create_switch-request"></a>处理 OID\_NIC\_SWITCH\_创建\_开关请求


NDIS 发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)来执行以下操作：

-   启用网络适配器上的 NIC 交换机，该适配器是由 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序静态创建的。 PF 是支持单根 i/o 虚拟化（SR-IOV）的网络适配器的硬件组件。

    从上下文中将一个 NIC 交换机静态创建为对[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用。 驱动程序将分配资源并基于从注册表设置中读取的参数创建开关。

-   在网络适配器上动态创建 NIC 交换机。

    如果 PF 微型端口驱动程序不支持静态 NIC 交换机创建，微型端口驱动程序将根据在 OID 请求中指定的参数分配资源并创建开关。

当 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，PF 微型端口驱动程序会公布其 sr-iov 接口支持。 如果 PF 微型端口驱动程序支持 SR-IOV，NDIS 将从注册表中读取 NIC 交换机配置。 在 NDIS\_NIC 发出 oid 的 OID 方法请求之前[\_交换机\_创建\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)到 PF 微型端口驱动程序，ndis 使用注册表将[**ndis\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)\_信息采用以下方式：

-   NDIS 将**SwitchType**成员设置为 NIC 交换机的类型。

    从 Windows Server 2012 开始，Windows 仅支持交换机类型**NdisNicSwitchTypeExternal**。 外部交换机指定连接到此类型的交换机的虚拟端口（VPorts）可以通过网络适配器上的物理端口访问外部网络。

    有关 NIC 交换机的详细信息，请参阅[Sr-iov 体系结构](sr-iov-architecture.md)。

-   NDIS 将**SwitchId**成员设置为 NIC 交换机的标识符值。 交换机标识符是一个介于零和网络适配器所支持的开关数之间的整数。 NDIS\_默认\_交换机\_ID 值指示默认 NIC 交换机。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的默认 NIC 交换机。

     

-   NDIS 设置**NumVFs**成员，该成员指定了 NIC 交换机上可分配的 PCIe 虚拟函数（VFs）的数目。

当接收到 oid\_NIC 的 OID 方法请求时[\_交换机\_创建\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态交换机创建和配置，它将在 NDIS 调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时创建 NIC 交换机。 当驱动程序处理此 OID 请求时，它必须验证 NDIS\_NIC 中的配置参数[ **\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 参数必须与驱动程序在调用*MiniportInitializeEx*期间使用的参数相同。 如果不是这样，则驱动程序必须使 OID 请求失败。

    有关详细信息，请参阅[创建 NIC 交换机的静态](static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态交换机创建和配置，则驱动程序必须验证[**NDIS\_NIC 的配置值\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构，并根据这些值创建 NIC 交换机。

    有关详细信息，请参阅[动态创建 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

3.  PF 小型端口驱动程序必须为 NIC 交换机上的默认 VPort 分配必要的硬件和软件资源。

    **请注意**  默认 VPort 始终通过 OID 的 oid 请求[\_NIC\_SWITCH\_创建\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)，并通过 oid\_\_\_[\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 [Oid\_nic 的 oid 请求\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)和[OID\_nic\_交换机\_DELETE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)用于在 nic 交换机上创建和删除非默认 VPorts。

     

4.  支持动态交换机创建和配置的 PF 微型端口驱动程序必须通过调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)在交换机上启用 sr-iov 虚拟化。 此调用在适配器的 PCI Express （PCIe）配置空间的 SR-IOV 扩展功能结构中配置**NumVFs**成员和**VF 启用**位。

    有关 SR-IOV 配置空间的详细信息，请参阅 PCI-SIG[单根 I/o 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)规范。

    **请注意**  如果 PF 微型端口驱动程序支持静态交换机创建，则在调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)时，它将启用 sr-iov 虚拟化。

     

如果 PF 微型端口驱动程序成功地 completesthe 了 oid\_NIC 的 OID 方法请求\_交换机\_创建\_交换机，则可以执行以下操作：

-   可以通过 oid\_NIC 的 oid 方法请求[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)来在 nic 交换机上分配 VFs。

-   可以通过 oid\_NIC 的 OID 方法请求[\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)创建非默认的 VPorts。

    微型端口驱动程序负责管理其非默认 VPorts 池。 驱动程序通过 NDIS\_NIC 的**NumVPorts**成员指定其池中的非默认 VPorts 数[ **\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。 驱动程序通过 oid [\_NIC\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)来返回此结构。

    **请注意**  网络适配器必须始终从其池中为 PF 创建默认 VPort。

     

 

 





