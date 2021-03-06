---
title: 发出 OID_NIC_SWITCH_ALLOCATE_VF 请求
description: 发出 OID_NIC_SWITCH_ALLOCATE_VF 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98cc3dc30337f9b70f198e555e047576a413088d
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249194"
---
# <a name="issuing-oid_nic_switch_allocate_vf-requests"></a>颁发 OID \_ NIC \_ 交换机 \_ 分配 \_ VF 请求


在 (OID 发出对象标识符之前，oid NIC 交换机的 ") 方法请求" 将 [ \_ \_ \_ \_ VF 分配](./oid-nic-switch-allocate-vf.md) 到 PCI Express (PCIe 的微型端口驱动程序) 物理函数 (PF) ，过量驱动程序将 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters) 结构格式化。 此结构包含要为网络适配器上的 (VF) 分配给 PCIe 虚拟函数的资源的配置参数。 过量驱动程序必须按以下方式设置此结构的成员：

-   **SwitchId** 成员必须设置为先前在网络适配器上创建的 NIC 交换机的标识符。 NIC 交换机是通过 oid [ \_ nic \_ 交换机 \_ CREATE \_ switch](./oid-nic-switch-create-switch.md)的 oid 方法请求创建的。

    当它处理 [oid \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 Oid 方法请求时，PCIe 物理函数的微型端口驱动程序 (PF) 为 VF 分配资源。 如果成功分配资源，PF 微型端口驱动程序会将 VF 分配给指定的 NIC 交换机。

    **注意**  从 Windows Server 2012 中的 NDIS 6.30 开始，SR-IOV 接口仅支持网络适配器上的默认 NIC 交换机。 **SwitchId** 成员的值必须设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

    有关 NIC 交换机的详细信息，请参阅 [Nic 交换机](nic-switches.md)。

-   **VFId** 成员必须设置为 NDIS 无效的 \_ \_ VF \_ 函数 \_ ID。

-   **RequestorId** 成员必须设置为 NDIS \_ 无效 \_ RID。

-   必须将 **VMFriendlyName** 和 **VMName** 成员设置为 hyper-v 子分区的参数。 PF 小型端口驱动程序仅出于信息目的使用这些成员。

    **注意**  Hyper-v 子分区也称为 *虚拟机 (VM)*。

    VF 与指定的 VM 相关联，而过量驱动程序发出 [OID \_ NIC \_ SWITCH \_ CREATE \_ SWITCH](./oid-nic-switch-create-switch.md) 请求。

-   **NicName** 成员必须设置为虚拟机 (VM) 网络适配器的标识符。 在 VM 中运行的来宾操作系统中公开了此虚拟适配器。 PF 小型端口驱动程序仅出于信息目的使用此成员。

    为 VF 分配资源并将其附加到子分区后，会在来宾操作系统中公开一个 VF 网络适配器。 VM 网络适配器组，其中包含用于通过基于硬件的 VF 数据路径进行数据包传输的 VF 网络适配器。

    但是，VF 可能与子分区分离，如在实时迁移过程中。 发生这种情况时，数据包传输通过基于软件的综合数据路径进行。 有关这些数据路径的详细信息，请参阅 [Sr-iov 数据路径](sr-iov-data-paths.md)。

-   必须将 **PermanentMacAddress** 和 **CurrentMacAddress** 成员设置为虚拟网络适配器 (MAC) 地址的媒体访问控制。 这些地址将公开给在 Hyper-v 子分区的来宾操作系统中运行的网络堆栈。

过量驱动程序发出 [oid \_ NIC \_ 交换机 \_ \_ ](./oid-nic-switch-allocate-vf.md) 的 oid 方法请求，方法是执行以下步骤：

1.  上层驱动程序为 OID 方法请求初始化 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构。 驱动程序将 **InformationBuffer** 成员设置为指向已初始化的 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters) 结构的指针。

2.  过量驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 将 OID 请求颁发给基础 PF 微型端口驱动程序。

    **注意**  当过量驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)时，ndis 会截获 OID 请求并验证 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters) 结构中指定的 VF 参数。 如果成功验证参数，NDIS 会将 OID 转发到 PF 微型端口驱动程序。 否则，NDIS 会失败，并且 NDIS \_ 状态 \_ 无效 \_ 参数。

在过量驱动程序为 VF 请求分配资源后，该驱动程序是唯一可请求为同一 VF 释放资源的组件。 过量驱动程序必须发出 oid [ \_ NIC \_ 交换机 \_ 自由 \_ vf](./oid-nic-switch-free-vf.md) 的 OID 设置请求，以释放 vf 资源。 在停止过量驱动程序之前，必须释放由驱动程序的 [OID \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md) 请求分配的每个 VF 的资源。
