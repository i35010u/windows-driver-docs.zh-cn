---
title: 处理 OID_NIC_SWITCH_CREATE_SWITCH 请求
description: 处理 OID_NIC_SWITCH_CREATE_SWITCH 请求
ms.assetid: 5C0BC300-8904-483A-A66B-8F5CFE0829B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8678960962fdfa6c3558bfc72d7fdc3b2fc2d0a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381341"
---
# <a name="handling-the-oidnicswitchcreateswitch-request"></a>处理 OID\_NIC\_交换机\_创建\_切换请求


NDIS 发出的一个对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)来执行以下操作：

-   启用静态创建的微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 的网络适配器上的 NIC 交换机。 PF 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的硬件组件。

    PF 微型端口驱动程序从上下文中调用静态创建 NIC 开关[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)。 该驱动程序分配的资源，并创建基于从注册表设置读取参数的开关。

-   网络适配器上动态创建一个 NIC 开关。

    如果 PF 微型端口驱动程序不支持静态 NIC 切换创建，微型端口驱动程序分配的资源，并创建基于 OID 请求中指定的参数的开关。

PF 微型端口驱动程序时 NDIS 调用驱动程序的播发其支持 SR-IOV 接口[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 如果 PF 微型端口驱动程序支持 SR-IOV，NDIS 从注册表中读取的 NIC 的交换机配置。 NDIS 发出 OID 方法请求的前[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)PF 微型端口驱动程序，到 NDIS 格式[ **NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构如下所示的注册表信息：

-   NDIS 集**SwitchType**成员添加到 NIC 交换机的类型。

    从 Windows Server 2012 开始，Windows 仅支持的某个交换机类型**NdisNicSwitchTypeExternal**。 外部交换机指定连接到此类型的交换机的虚拟端口 (VPorts) 可以通过网络适配器上的物理端口访问外部网络。

    有关 NIC 开关的详细信息，请参阅[SR-IOV 体系结构](sr-iov-architecture.md)。

-   NDIS 集**SwitchId**成员添加到 NIC 开关的标识符值。 交换机标识符是零到的网络适配器支持的切换数之间的整数。 NDIS\_默认\_切换\_ID 值表示默认 NIC 开关。

    **请注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持的默认 NIC 切换上的网络适配器。

     

-   NDIS 集**NumVFs**成员，用于指定数目的 PCIe 虚拟函数 (VFs)，它可以分配的 NIC 上切换。

当它收到的 OID 方法请求[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态交换机创建和配置，它创建 NIC 开关，当调用 NDIS [ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)。 当驱动程序处理此 OID 请求时，它必须验证中的配置参数[ **NDIS\_NIC\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构。 参数必须与使用的驱动程序以在调用期间创建的交换机相同*MiniportInitializeEx*。 如果不为 true，则驱动程序必须失败 OID 请求。

    有关详细信息，请参阅[静态创建的 NIC 交换机](static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态交换机创建和配置，该驱动程序必须验证的配置值[ **NDIS\_NIC\_切换\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters)结构并创建 NIC 交换机基于这些值。

    有关详细信息，请参阅[动态创建的 NIC 交换机](dynamic-creation-of-a-nic-switch.md)。

3.  PF 微型端口驱动程序必须为 NIC 交换机上的默认 VPort 分配所需的硬件和软件资源。

    **请注意**  VPort 始终通过 OID 请求的创建的默认[OID\_NIC\_开关\_创建\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)，删除通过 OID请求的[OID\_NIC\_交换机\_删除\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 OID 请求[OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)并[OID\_NIC\_交换机\_删除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)用于创建和删除 NIC 交换机上的非默认 VPorts。

     

4.  支持动态交换机创建和配置 PF 微型端口驱动程序必须通过调用启用 SR-IOV 交换机上的虚拟化[ **NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization)。 此调用将配置**NumVFs**成员和**VF 启用**位中的 SR-IOV 扩展功能的适配器的 PCI Express (PCIe) 配置空间。

    有关 SR-IOV 配置空间的详细信息，请参阅 PCI SIG[单根 I/O 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)规范。

    **请注意**  如果 PF 微型端口驱动程序支持静态交换机创建，它将启用 SR-IOV 虚拟化后创建开关时[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)称为.

     

如果 PF 微型端口驱动程序已成功 completesthe OID 方法请求的 OID\_NIC\_交换机\_创建\_开关，它允许发生以下情况：

-   可以分配 VFs 通过 OID 方法请求的 NIC 交换机上[OID\_NIC\_切换\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

-   可以创建非默认 VPorts 通过 OID 方法请求的 NIC 交换机上[OID\_NIC\_切换\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

    微型端口驱动程序负责管理自己的非默认 VPorts 池。 该驱动程序指定其池中的非默认 VPorts 数通过**NumVPorts**的成员[ **NDIS\_NIC\_开关\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。 驱动程序将返回通过 OID 查询请求的此结构[OID\_NIC\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)。

    **请注意**  网络适配器必须始终默认 VPort 从其池为创建 PF.

     

 

 





