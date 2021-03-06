---
title: 管理发往物理网络适配器的硬件卸载 OID 请求
description: 管理发往物理网络适配器的硬件卸载 OID 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd915aecedf5819ae710a6a20cd0b0f38af89f95
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248111"
---
# <a name="managing-hardware-offload-oid-requests-to-physical-network-adapters"></a>管理发往物理网络适配器的硬件卸载 OID 请求


本主题讨论了如何通过可扩展交换机控制路径，将 Hyper-v 可扩展交换机转发扩展管理 (OID 上的对象标识符，) 对底层物理适配器上的硬件卸载技术的请求。

例如，可以将外部网络适配器绑定到 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟端口边缘。 MUX 驱动程序绑定到主机上一个或多个物理网络的团队。 此配置称为 *可扩展交换机团队*。

在此配置中，可扩展交换机扩展将公开给团队中的每个网络适配器。 这允许该扩展管理团队中各个网络适配器的配置和使用。 例如，转发扩展可以通过将传出数据包转发到各个适配器，为负载平衡故障转移 (LBFO) 解决方案提供支持。 管理可扩展交换机团队的转发扩展称为 *组合提供程序*。 有关组合提供程序的详细信息，请参阅 [组合提供程序扩展](teaming-provider-extensions.md)。

下图显示了 (Windows Server 2012 R2) 和更高版本的 NDIS 6.40 的可扩展交换机团队示例。

![用于 ndis 6.40 的可扩展交换机团队示意图](images/vswitch-oid-controlpath2-ndis640.png)

下图显示了 (Windows Server 2012) 的 NDIS 6.30 的可扩展交换机团队示例。

![用于 ndis 6.30 的可扩展交换机团队示意图](images/vswitch-oid-controlpath2.png)

**注意**  在可扩展交换机接口中，NDIS 筛选器驱动程序称为 *可扩展交换机扩展* ，驱动程序堆栈称为 *可扩展交换机驱动程序堆栈*。

 

通过处理 [oid \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md)的 oid 请求，转发扩展可以参与可扩展交换机团队的配置以实现硬件卸载。 例如，如果扩展管理可扩展交换机团队的物理网络适配器，则可以将 OID \_ 交换机 \_ NIC \_ 请求请求转发到支持硬件卸载的物理适配器。

NDIS 和过量协议以及筛选器驱动程序可以向底层物理网络适配器发出对硬件卸载技术的 OID 请求。 当这些 OID 请求到达可扩展交换机接口时，它将在 [**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)中封装 oid 请求。 然后，可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md) 的 oid 请求，其中包含此结构。

可扩展交换机接口封装以下硬件卸载技术的 Oid：

<a href="" id="internet-protocol-security--ipsec--offload--version-2-"></a>Internet 协议安全 (IPsec) 卸载 (版本 2)   
以下 IPsec OID 请求被封装：

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md)

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA \_ EX](./oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ DELETE \_ SA](./oid-tcp-task-ipsec-offload-v2-delete-sa.md)

-   [OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 更新 \_ SA](./oid-tcp-task-ipsec-offload-v2-update-sa.md)

转发扩展不能 *失败或拒绝* 这些 OID 请求。

有关 IPsec 硬件卸载技术版本2的详细信息，请参阅 [Ipsec 卸载版本 2](./introduction-to-ipsec-offload-version-2.md)。

<a href="" id="single-root-i-o-virtualization--sr-iov-"></a>单个根 i/o 虚拟化 (SR-IOV)   
以下 SR-IOV OID 请求被封装：

-   [OID \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)

-   [OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)

-   [OID \_ NIC \_ 交换机 \_ 删除 \_ VPORT](./oid-nic-switch-delete-vport.md)

-   [OID \_ NIC \_ 交换机 \_ 免费 \_ VF](./oid-nic-switch-free-vf.md)

-   [OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md)

-   [OID \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md)

转发扩展可以通过使用不是 NDIS 状态成功的状态代码来完成请求，拒绝 [oid \_ nic \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md) 和 [oid \_ nic \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md) 的 oid 请求 \_ \_ 。 但是，扩展不能否决其他 SR-IOV OID 请求。

有关 SR-IOV 硬件卸载技术的详细信息，请参阅 [单一根 I/o 虚拟化 (sr-iov) ](single-root-i-o-virtualization--sr-iov-.md)。

<a href="" id="virtualized-machine-queue--vmq-"></a>虚拟机队列 (VMQ)   
以下 VMQ OID 请求被封装：

-   [OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md)

-   [OID \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md)

-   [OID \_ 接收 \_ 筛选器 \_ 可用 \_ 队列](./oid-receive-filter-free-queue.md)

-   [OID \_ 接收 \_ 筛选器 \_ 队列 \_ 分配 \_ 完成](./oid-receive-filter-queue-allocation-complete.md)

-   [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)

转发扩展可以通过使用不是 NDIS 状态成功的状态代码完成请求来否决 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md) 和 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md) 的 oid 请求 \_ \_ 。 但是，扩展不能否决其他 VMQ OID 请求。

有关 VMQ 硬件卸载技术的详细信息，请参阅 [ (vmq) 虚拟机队列 ](virtual-machine-queue--vmq-.md)。

转发扩展必须遵循以下准则来处理硬件卸载 OID 请求：

-   Microsoft IM 平台仅公布了整个团队的常见卸载功能。 但是，扩展可以生成 OID 请求，以查询团队中每个适配器的功能。

    一旦扩展确定了组中物理适配器的硬件功能，它就可以将硬件卸载的 OID 集请求转发到最适合卸载的适配器。

-   通过过量协议或筛选器驱动程序发出的所有硬件卸载 OID 请求将封装在 [**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request) 结构内。 转发扩展发出的所有硬件卸载 OID 请求也必须封装在 **NDIS \_ 交换机 \_ NIC \_ OID \_ 请求** 结构中。

    扩展通过 oid [ \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md)的 oid 设置请求，将封装的 OID 请求转发到基础物理网络适配器。 有关此过程的详细信息，请参阅 [将 OID 请求转发到物理网络适配器](forwarding-oid-requests-to-physical-network-adapters.md)。

-   扩展不能修改或失败硬件卸载 OID 请求以清除、释放或完成卸载资源的分配。 例如，扩展不得失败 [oid \_ 接收 \_ 筛选器 \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md) 或 [oid \_ NIC \_ SWITCH \_ DELETE \_ VPORT](./oid-nic-switch-delete-vport.md)的 oid 请求。 可扩展交换机接口必须处理这些 OID 请求，才能清理这些资源的状态信息。

    扩展可以修改或失败硬件卸载 OID 请求，以分配、移动或设置卸载资源。 例如，扩展可能会失败或修改 [oid \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md) 或 [oid \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ ADD \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md)的 oid 请求。

-   此扩展可以从任何硬件卸载 Oid 到基础物理网络适配器。 但是，扩展不能产生清除或释放扩展未分配的卸载资源的硬件卸载 OID。

    例如，如果不是为同一队列的[oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md)请求，则扩展不能产生[oid \_ 接收 \_ 筛选器 \_ 免费 \_ 队列](./oid-receive-filter-free-queue.md)的硬件卸载 oid 请求。

    **注意**  如果扩展正在筛选过量驱动程序发出的同一 OID 请求，则该扩展只能产生自己的封装硬件卸载 OID 请求。 在这种情况下，扩展不能转发原始 OID 请求。 相反，该扩展插件必须调用 [**NdisFOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete) ，以便在 NDIS 调用其 [*FilterOidRequestComplete*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) 来完成发起的 OID 请求时完成此请求。

     

-   如果扩展插件将硬件卸载 OID 请求转发到基础物理网络适配器，则必须将 [**NDIS \_ 交换机 \_ NIC \_ Oid \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构的 **DestinationNicIndex** 成员设置为该适配器的非零索引值。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](network-adapter-index-values.md)。

    此外， **DestinationPortId** 成员必须设置为外部网络适配器连接到的可扩展交换机端口的标识符。

-   如果扩展插件产生硬件卸载 OID 请求来为 Hyper-v 子分区分配资源，则必须将 [**NDIS \_ 交换机 \_ NIC \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构的 **SourcePortId** 成员设置为分区连接到的可扩展交换机端口的标识符。

    **SourceNicIndex** 成员必须设置为 **NDIS \_ SWITCH \_ DEFAULT \_ NIC \_ INDEX**。

-   当扩展调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)转发 OID 请求时，它必须将 *OidRequest* 参数设置为指向 [oid \_ 交换机 \_ NIC \_ 请求](./oid-switch-nic-request.md)oid 请求的 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的指针。

有关扩展如何筛选 OID 请求的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关 MUX 驱动程序的详细信息，请参阅 [NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

