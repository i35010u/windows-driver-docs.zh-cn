---
title: 发出 OID_NIC_SWITCH_ALLOCATE_VF 请求
description: 发出 OID_NIC_SWITCH_ALLOCATE_VF 请求
ms.assetid: 72285E72-DEC7-4578-9B6C-E616FECD6F41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 619f0f31f651afecfd2258909c79b4eb49396ce7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844154"
---
# <a name="issuing-oid_nic_switch_allocate_vf-requests"></a>颁发 OID\_NIC\_交换机\_分配\_VF 请求


在发出 OID\_NIC 的对象标识符（OID）方法请求之前[\_交换机\_将\_VF 分配](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)给 PCI Express （PCIe）物理函数（PF）的微型端口驱动程序，过量驱动程序将 NDIS 设置为格式[ **\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 此结构包含要为网络适配器上的 PCIe 虚拟功能（VF）分配的资源的配置参数。 过量驱动程序必须按以下方式设置此结构的成员：

-   **SwitchId**成员必须设置为先前在网络适配器上创建的 NIC 交换机的标识符。 NIC 交换机是通过 oid\_NIC 的 oid 方法请求创建的[\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)。

    当它处理 Oid\_NIC 的 OID 方法请求时[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)时，PCIe 物理功能（PF）的微型端口驱动程序为 vf 分配资源。 如果成功分配资源，PF 微型端口驱动程序会将 VF 分配给指定的 NIC 交换机。

    **注意** 从 Windows Server 2012 中的 NDIS 6.30 开始，SR-IOV 接口仅支持网络适配器上的默认 NIC 交换机。 **SwitchId**成员的值必须设置为 NDIS\_默认\_交换机\_ID。

    有关 NIC 交换机的详细信息，请参阅[Nic 交换机](nic-switches.md)。

-   **VFId**成员必须设置为 NDIS\_无效\_VF\_函数\_ID。

-   **RequestorId**成员必须设置为 NDIS\_无效\_RID。

-   必须将**VMFriendlyName**和**VMName**成员设置为 hyper-v 子分区的参数。 PF 小型端口驱动程序仅出于信息目的使用这些成员。

    **注意** Hyper-v 子分区也称为*虚拟机（VM）* 。

    VF 与指定的 VM 相关联，而过量驱动程序发出[OID\_NIC\_交换机\_创建\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)请求。

-   **NicName**成员必须设置为虚拟机（VM）网络适配器的标识符。 在 VM 中运行的来宾操作系统中公开了此虚拟适配器。 PF 小型端口驱动程序仅出于信息目的使用此成员。

    为 VF 分配资源并将其附加到子分区后，会在来宾操作系统中公开一个 VF 网络适配器。 VM 网络适配器组，其中包含用于通过基于硬件的 VF 数据路径进行数据包传输的 VF 网络适配器。

    但是，VF 可能与子分区分离，如在实时迁移过程中。 发生这种情况时，数据包传输通过基于软件的综合数据路径进行。 有关这些数据路径的详细信息，请参阅[Sr-iov 数据路径](sr-iov-data-paths.md)。

-   必须将**PermanentMacAddress**和**CurrentMacAddress**成员设置为 VF 虚拟网络适配器的媒体访问控制（MAC）地址。 这些地址将公开给在 Hyper-v 子分区的来宾操作系统中运行的网络堆栈。

通过执行以下步骤，过量驱动程序会发出 Oid\_NIC 的 oid 方法请求[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf) ：

1.  上层驱动程序为 OID 方法请求初始化[**NDIS\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。 驱动程序将**InformationBuffer**成员设置为指向已初始化[**NDIS\_NIC 的指针\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

2.  过量驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)将 OID 请求颁发给基础 PF 微型端口驱动程序。

    **注意** 当过量驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)时，ndis 会截获 OID 请求，并验证 NDIS\_NIC 中指定的 VF 参数[ **\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 如果成功验证参数，NDIS 会将 OID 转发到 PF 微型端口驱动程序。 否则，NDIS 会将具有 NDIS\_状态的 OID 请求\_无效\_参数。

在过量驱动程序为 VF 请求分配资源后，该驱动程序是唯一可请求为同一 VF 释放资源的组件。 过量驱动程序必须发出 oid\_NIC 的 OID 集请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VF 资源。 在可以停止过量驱动程序之前，它必须释放由驱动程序的 OID\_NIC 分配的每个 VF 的资源[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)请求。