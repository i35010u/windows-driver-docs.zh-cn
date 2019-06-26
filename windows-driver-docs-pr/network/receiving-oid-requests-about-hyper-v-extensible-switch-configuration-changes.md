---
title: 接收的 HYPER-V 可扩展交换机配置更改 OID 请求
description: 接收有关 Hyper-V 可扩展交换机配置更改的 OID 请求
ms.assetid: 9149BFF3-59B3-4563-A1A1-34FDD115964E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9e7b9ef5dbb5c9d2fd59a8e153bd2b01be51470
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385428"
---
# <a name="receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes"></a>接收有关 Hyper-V 可扩展交换机配置更改的 OID 请求

可扩展交换机接口通知有关对可扩展交换机组件配置更改的基础扩展，并通过发出可扩展的策略参数切换对象标识符 (OID) 的集请求。 这些请求颁发的可扩展的交换机，以通知有关更改的可扩展交换机组件配置和策略参数的基础扩展的协议边缘。 这些 OID 请求将通过可扩展交换机驱动程序堆栈移到可扩展交换机的基础的微型端口边缘。

下图显示了 OID 请求 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机控制路径。

![ndis 6.40 的 vswitch oid 控制路径的关系图](images/vswitch-oid-controlpath-ndis640.png)

下图显示 OID 请求的可扩展交换机控制的路径的 NDIS 6.30 (Windows Server 2012)。

![ndis 6.30 的 vswitch oid 控制路径的关系图](images/vswitch-oid-controlpath.png)

**请注意**可扩展交换机接口，在 NDIS 筛选器驱动程序被称为*可扩展交换机扩展*驱动程序堆栈称为*可扩展交换机驱动程序堆栈*。 

可扩展交换机的协议边缘发出通知的以下类型的 OID 集请求：

-   对可扩展的交换机上的端口配置的更改。

    例如，协议驱动程序问题[OID\_切换\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)以通知有关的可扩展交换机上的端口创建的基础扩展。 同样，协议驱动程序问题[OID\_交换机\_端口\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)以通知有关端口的删除扩展。

    有关此类型的 OID 通知的详细信息，请参阅[HYPER-V 可扩展交换机端口](hyper-v-extensible-switch-ports.md)。

-   可扩展的交换机上的端口的网络适配器连接到的更改。

    例如，协议驱动程序问题[OID\_切换\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)通知可扩展交换机上的端口的网络适配器的连接有关的基础扩展。 同样，协议驱动程序问题[OID\_交换机\_NIC\_断开连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)通知扩展已断开网络适配器连接从端口。

    有关此类型的 OID 通知的详细信息，请参阅[HYPER-V 可扩展交换机的网络适配器](hyper-v-extensible-switch-network-adapters.md)。

-   可扩展交换机端口或交换机策略的更改。

    例如，协议驱动程序问题[OID\_切换\_属性\_添加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)以通知有关添加可扩展交换机属性的基础扩展。 同样，协议驱动程序问题[OID\_交换机\_端口\_属性\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)以通知有关端口属性删除扩展。

    有关此类型的 OID 通知的详细信息，请参阅[管理的 HYPER-V 可扩展交换机策略](managing-hyper-v-extensible-switch-extensibility-policies.md)。

    **请注意**扩展不通过可扩展交换机的基础的微型端口边缘通知对进行管理的默认端口或交换机策略的更改。

-   保存或恢复运行时端口数据。

    例如，协议驱动程序问题[OID\_切换\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)通知基础扩展来将指定的端口的运行时数据保存在可扩展的交换机上。 这些 Oid 颁发 HYPER-V 状态时保存或迁移到另一台主机。 同样，协议驱动程序问题[OID\_切换\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)以通知运行时端口数据要还原在可扩展的交换机上的扩展。

    有关此类型的 OID 通知的详细信息，请参阅[管理的 HYPER-V 可扩展交换机运行时数据](managing-hyper-v-extensible-switch-run-time-data.md)。

可扩展的交换机扩展微型端口驱动程序负责完成这些 OID 请求。 但是，某些可扩展交换机 OID 请求，与基础扩展可能失败的 OID 请求来禁止通知。 例如，当可扩展交换机协议驱动程序通知有关将可扩展交换机创建的新端口的筛选器驱动程序，它发出的 OID 集请求[OID\_切换\_端口\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create). 基础筛选或转发扩展可通过完成状态为 OID 请求否决端口创建\_数据\_不\_已接受。

可扩展的交换机扩展必须遵循这些准则时其[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)可扩展交换机 OID 请求调用函数：

-   该扩展不能修改所指向的任何数据*OidRequest*参数。

-   对于某些可扩展交换机 OID 请求，该扩展可以完成状态为 OID 请求\_数据\_不\_已接受。 这 vetoes 上为其颁发的 OID 请求一个可扩展交换机组件的操作。

    例如，扩展可以完成[OID\_交换机\_NIC\_创建](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)状态请求\_数据\_不\_已接受。 该驱动程序可能需要执行此操作，如果它不能满足其指定为其创建的网络连接的端口上配置的策略。

    该扩展可以为以下 Oid 完成这种方式中的请求：

    -   [OID\_SWITCH\_NIC\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)

    -   [OID\_SWITCH\_PORT\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)

    -   [OID\_SWITCH\_PORT\_PROPERTY\_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)

    -   [OID\_SWITCH\_PORT\_PROPERTY\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)

    -   [OID\_SWITCH\_PORT\_PROPERTY\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)

    -   [OID\_SWITCH\_PROPERTY\_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)

    -   [OID\_SWITCH\_PROPERTY\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)

    -   [OID\_SWITCH\_PROPERTY\_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)

-   如果扩展不会完成 OID 请求，它必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)可扩展交换机在驱动程序堆栈的下层将请求转发。

    **请注意**驱动程序调用之前[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)，该驱动程序必须调用[ **NdisAllocateCloneOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatecloneoidrequest)到分配[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构，并将请求信息传输到新的结构。

    该扩展应监视的 OID 完成结果请求时其[ *FilterOidRequestComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete)调用函数。 这样，要确定可扩展交换机组件上的操作已成功完成还是基础扩展被否决的扩展。

    有关如何筛选和 OID 请求转发的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。


-   NDIS 和基础协议和筛选器驱动程序可以发出硬件卸载技术的 OID 请求到基础物理网络适配器。 这包括卸载技术，例如虚拟机队列 (VMQ)、 Internet 协议安全 (IPsec) 和单根 I/O 虚拟化 (SR-IOV) 的 OID 请求。

    当这些 OID 请求在可扩展交换机接口，它封装在 OID 请求[ **NDIS\_切换\_NIC\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request). 然后，可扩展交换机的协议边缘颁发的 OID 请求[OID\_切换\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)，其中包含此结构。

-   转发扩展的可扩展交换机可以绑定到外部网络适配器的一个或多个物理适配器上的 NDIS 硬件卸载技术提供支持。 在此配置中，可扩展交换机外部网络适配器绑定到的 NDIS 多路复用器 (MUX) 中间驱动程序的虚拟微型端口边缘。 MUX 中间驱动程序绑定到一个或多个物理网络的团队在主机上。 此配置称为*可扩展交换机团队*。 有关可扩展交换机团队详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

    在此配置中，可扩展交换机扩展公开给团队中每个网络适配器。 这样，转发扩展中要管理的配置和使用的团队中的单个网络适配器的可扩展交换机驱动程序堆栈。 例如，该扩展插件可以为负载平衡团队通过故障转移 (LBFO) 解决方案，通过将传出数据包转发到各个适配器提供支持。 此类扩展被称为*组合的提供程序*。 有关组合提供程序的详细信息，请参阅[组合提供程序扩展](teaming-provider-extensions.md)。

    通过处理 OID 请求的[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)，组合提供程序可以参与硬件卸载功能的适配器组的配置。 例如，扩展可以生成自己的 OID 的 OID 请求\_交换机\_NIC\_请求参数的硬件配置的物理适配器卸载。

    有关如何处理的详细信息[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)OID 请求，请参阅[转发到物理网络适配器的 OID 请求](forwarding-oid-requests-to-physical-network-adapters.md)。

    **请注意**扩展筛选器驱动程序可以生成的 OID 请求[OID\_交换机\_NIC\_请求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)向绑定到可扩展任何物理适配器发出的私有 Oid切换外部网络适配器。

**请注意**堆栈的重新启动请求使用[ **NdisFRestartFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfrestartfilter)可扩展交换机 OID 请求挂起时，将不会完成。 出于此原因，正在等待堆栈重新启动的扩展必须完成任何正在进行的 OID 请求。

可扩展交换机 OID 请求的控制路径的详细信息，请参阅[HYPER-V 可扩展交换机控件路径的 OID 请求](hyper-v-extensible-switch-control-path-for-oid-requests.md)。









