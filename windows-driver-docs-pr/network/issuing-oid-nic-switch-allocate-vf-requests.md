---
title: 发出 OID_NIC_SWITCH_ALLOCATE_VF 请求
description: 发出 OID_NIC_SWITCH_ALLOCATE_VF 请求
ms.assetid: 72285E72-DEC7-4578-9B6C-E616FECD6F41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f5ee761d0222aedd6f8984ef09b73ba0e88c72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356260"
---
# <a name="issuing-oidnicswitchallocatevf-requests"></a>发出 OID\_NIC\_交换机\_分配\_VF 请求


它会发出对象标识符 (OID) 方法请求的前[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)微型端口驱动程序为 PCI Express (PCIe) 物理函数 () pf，PF过量的驱动程序格式[ **NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 此结构包含的资源，并将其分配为 PCIe 虚拟函数 (VF) 上的网络适配器的配置参数。 基础驱动程序必须按以下方式设置此结构的成员：

-   **SwitchId**成员必须设置为先前创建的网络适配器的 NIC 交换机的标识符。 通过 OID 方法请求的创建 NIC 交换机[OID\_NIC\_切换\_创建\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。

    当它处理的 OID 方法请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)，微型端口驱动程序 PCIe 物理函数 (PF) 用于为 VF 分配资源。 如果已成功分配资源，PF 微型端口驱动程序将 VF 分配给指定 NIC 的交换机。

    **请注意**从 Windows Server 2012 中的 NDIS 6.30 开始，SR-IOV 接口仅支持的默认 NIC 切换上的网络适配器。 值**SwitchId**成员必须设置为 NDIS\_默认\_交换机\_id。

    在 NIC 的交换机上的详细信息，请参阅[NIC 开关](nic-switches.md)。

-   **VFId**成员必须设置为 NDIS\_无效\_VF\_函数\_id。

-   **RequestorId**成员必须设置为 NDIS\_无效\_RID。

-   **VMFriendlyName**并**VMName**成员必须设置为 HYPER-V 子分区的参数。 PF 微型端口驱动程序使用这些成员仅用于提供信息。

    **请注意**HYPER-V 子分区是也称为*虚拟机 (VM)* 。

    VF 是与基础驱动程序问题之前指定的 VM 相关联[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求。

-   **NicName**成员必须设置为虚拟机 (VM) 网络适配器的标识符。 此虚拟适配器公开在 VM 中运行来宾操作系统中。 PF 微型端口驱动程序使用此成员仅用于提供信息。

    当 VF 分配资源并附加到子分区时，来宾操作系统中公开 VF 网络适配器。 VM 网络适配器与 VF 网络适配器的数据包传输团队通过基于硬件的 VF 数据路径。

    但是，取景器无法从分离子分区中，如实时迁移过程。 在此情况下，通过基于软件的综合数据路径进行，数据包传输。 这些数据路径的详细信息，请参阅[SR-IOV 数据路径](sr-iov-data-paths.md)。

-   **PermanentMacAddress**并**CurrentMacAddress**成员都必须设置为媒体 VF 的虚拟网络适配器的访问控制 (MAC) 地址。 这些地址公开运行 HYPER-V 子分区的来宾操作系统中的网络堆栈。

基础驱动程序将发出的 OID 方法请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)通过执行以下步骤：

1.  基础驱动程序初始化[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 方法请求的结构。 驱动程序集**InformationBuffer**指向一个已初始化的指针到成员[ **NDIS\_NIC\_开关\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

2.  过量的驱动程序调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest) OID 请求发出到基础 PF 微型端口驱动程序。

    **请注意**过量的驱动程序在调用[ **NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)，NDIS 截获的 OID 请求，并验证中指定的 VF 参数[ **NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 如果成功验证了参数，NDIS 将转发到 PF 微型端口驱动程序的 OID。 否则，NDIS 将会失败 OID NDIS\_状态\_无效\_参数。

基础驱动程序请求 VF 的资源分配后，该驱动程序将是可以请求的同一 VF 释放资源的唯一组件。 基础驱动程序必须发出的 OID 集请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VF 资源。 可以暂停基础驱动程序之前，它必须释放资源的已分配的驱动程序的每个 VF [OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)请求。