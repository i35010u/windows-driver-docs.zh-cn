---
title: 组合提供程序扩展
description: 组合提供程序扩展
ms.assetid: 94F73ECD-54D0-4218-B3C4-33DC3BD57ED0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93328b8029926992574ab1d18f72d7a898c963d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841781"
---
# <a name="teaming-provider-extensions"></a>组合提供程序扩展


可扩展交换机外部网络适配器可以绑定到 NDIS 多路复用器（MUX）中间驱动程序的虚拟微型端口边缘。 MUX 中间驱动程序本身可以绑定到主机上一个或多个物理网络的团队。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队的详细信息，请参阅[物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

在此配置中，可扩展交换机扩展会公开给可扩展交换机团队中的每个网络适配器。 这允许可扩展交换机驱动程序堆栈中的转发扩展管理团队中单个网络适配器的配置和使用。 例如，扩展可以通过将传出数据包转发到各个适配器，为团队提供负载平衡故障转移（LBFO）解决方案的支持。 此类扩展称为*组合提供程序*。

下图显示了与基本可扩展交换机团队（绑定到 NDIS 6.40 （Windows Server 2012 R2）和更高版本）的外部网络适配器的数据包流量的数据路径。

![从 vswitch 团队传入或向其绑定到 ndis 6.40 的外部网络适配器的数据包流量的数据路径](images/vswitchteam-ndis640.png)

下图显示了与基本可扩展交换机团队（绑定到 NDIS 6.30 （Windows Server 2012）的外部网络适配器）之间的数据包流量的数据路径。

![从 vswitch 团队传入或向其绑定到 ndis 6.30 的外部网络适配器的数据包流量的数据路径](images/vswitchteam.png)

组合提供程序可执行转发扩展可以执行的所有操作。 此外，组合提供程序可以执行以下操作。

-   将传出数据包转发到可扩展交换机团队中的单个物理适配器。 此功能对 LBFO 功能特别有用。

-   将标准 NDIS 对象标识符（OID）请求转发到可扩展交换机组中的单个物理适配器。 此功能对于在组中配置硬件卸载的适配器尤为有用。

    例如，MUX 驱动程序会公布整个可扩展交换机团队的常见功能。 但是，组合提供程序可以发出 OID 请求，以查询组内适配器的各个功能。 然后，组合提供程序可以向可扩展交换机外部网络适配器发出 OID 请求，以设置适用于整个团队的功能。

-   将专用 OID 请求转发到可扩展交换机团队中的单个物理适配器。 这些专用 OID 请求由独立硬件供应商（IHV）为物理网络适配器定义。 这允许由 IHV 开发的组合提供程序启用或禁用组中单个物理适配器上的专有属性。

-   从可扩展交换机团队修改 NDIS 状态指示。 此功能对于管理用于硬件卸载的可扩展交换机团队特别有用。

    例如，MUX 驱动程序会发出 NDIS 状态指示，其中包含整个可扩展交换机团队公用的设置。 如果为可扩展交换机团队中的网络适配器启用了组合提供程序的硬件卸载的状态指示，则组合提供程序可以首先发出 OID 请求，以查询该适配器上的当前功能。 然后，组合提供程序可以修改指示数据，以设置可能已在适配器上更改的那些属性。

在管理可扩展交换机团队时，组合提供程序必须遵循以下准则：

-   组合提供程序必须为已建立可扩展交换机网络连接的每个物理网络适配器维护状态。

    对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘将[\_NIC\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)的单独 oid 集请求颁发\_交换机。 此 OID 请求通知扩展有关创建到基础物理适配器的网络连接的信息。

-   当创建到物理网络适配器的网络连接时，将为其分配一个非零索引值，此值对于连接外部网络适配器的端口是唯一的。

    当组提供程序发出数据包或将其转发到基础物理网络适配器的请求时，它必须指定网络适配器索引值。

    有关详细信息，请参阅[网络适配器索引值](network-adapter-index-values.md)。

-   如果组合提供程序出现问题或将数据包转发给物理适配器，则必须指定物理适配器连接的非零网络适配器索引值。

    当提供程序接收数据包时，它可以根据[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中数据包的带外转发上下文确定源网络适配器索引值\_列表结构。 有关转发上下文的详细信息，请参阅[Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

    有关详细信息，请参阅[Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

-   若要对物理适配器发出转发 OID 请求，组合提供程序必须在[**NDIS\_交换机\_NIC\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)结构中封装 OID 请求。 提供程序必须将**DestinationNicIndex**成员设置为物理适配器连接的非零网络适配器索引值。 然后，提供程序发出 oid [\_SWITCH\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)的 oid 集请求，\_请求将封装的 OID 请求传递给目标物理适配器。

    有关详细信息，请参阅[管理对物理网络适配器的 OID 请求](managing-oid-requests-to-physical-network-adapters.md)。

-   组合提供程序可以代表基础物理适配器发出 NDIS 状态指示。 要执行此操作，提供程序必须将[ **\_NIC\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)结构中的指示封装到 NDIS\_交换机中。 提供程序必须将**SourceNicIndex**成员设置为物理适配器连接的非零网络适配器索引值。 然后，提供程序发出 ndis 状态指示， [ **\_状态\_交换机\_NIC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)，以便将封装的状态指示传递到可扩展交换机驱动程序堆栈中的过量驱动程序。

    有关详细信息，请参阅[从物理网络适配器管理 NDIS 状态指示](managing-ndis-status-indications-from-physical-network-adapters.md)。

有关转发扩展的详细信息，请参阅[转发扩展](forwarding-extensions.md)。

有关 MUX 驱动程序的详细信息，请参阅[NDIS MUX 中间驱动程序](ndis-mux-intermediate-drivers.md)。

 

 





