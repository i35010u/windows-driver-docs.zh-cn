---
title: Hyper-V 可扩展交换机还原操作
description: Hyper-V 可扩展交换机还原操作
ms.assetid: 283D9E43-79F2-47B1-8D29-39A8E7CBE2C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9942b3b79ab63a02664b58e1e769f67f6257a01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384555"
---
# <a name="hyper-v-extensible-switch-restore-operations"></a>Hyper-V 可扩展交换机还原操作


它已停止或实时迁移后，重新启动 HYPER-V 子分区时，还原的分区的运行时状态。 在还原操作时，HYPER-V 可扩展交换机扩展驱动程序可以还原有关可扩展交换机网络适配器 (NIC) 的运行时数据。

当还原操作正在执行上的 HYPER-V 子分区，可扩展交换机接口发出信号的可扩展交换机的协议边缘发出 OID 设置的请求[OID\_切换\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 的结构\_交换机\_NIC\_还原请求包含的指针[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。

当它处理此 OID 请求时，该扩展将还原的网络适配器的运行时数据。 此运行时数据以前保存的 OID 请求通过[OID\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)和 OID\_开关\_NIC\_保存\_完成。

当它收到[OID\_切换\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)请求，可扩展交换机扩展必须首先确定它是否拥有的运行时数据。 该驱动程序通过实现这一点将的值进行比较**ExtensionId**的成员[ **NDIS\_开关\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)驱动程序使用来标识自身的 GUID 值的结构。

如果该扩展拥有的运行时数据，它可按以下方式恢复此数据：

1.  扩展可将复制中的运行时数据**SaveData**成员添加到驱动程序分配存储。

    **请注意**  的值**PortId**的成员[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构可能不同于**PortId**处运行时数据已保存的时间值。 如果运行时数据从一个主机到另一个保存在实时迁移期间，这可能发生。 但是，在实时迁移期间保留的可扩展交换机 NIC 配置。 这样，扩展插件可以使用新的运行时数据还原到可扩展交换机 NIC **PortId**值。

     

2.  扩展完成 OID 集请求使用 NDIS\_状态\_成功。

如果扩展不拥有的运行时数据，它必须调用[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)。 这 OID 方法将请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)  
可扩展交换机接口发出信号发出的可扩展交换机 nic。 运行时数据的还原操作完成时此 OID 的可扩展交换机的协议边缘

此 OID 请求通知的扩展的还原操作已完成仅对指定的可扩展交换机 nic。

有关此 OID 请求的详细信息，请参阅[OID\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)。

在还原操作的运行时数据时，可扩展交换机的协议边缘发出的 OID 请求[OID\_切换\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)并[OID\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)为网络接口的 HYPER-V 子分区连接。 如果还原多个 HYPER-V 子分区，分别设置的 OID 协议边缘发出\_交换机\_NIC\_还原和 OID\_交换机\_NIC\_还原\_完成每个网络接口连接的请求。

**请注意**  可扩展交换机的协议边缘会交替执行还原操作的运行时数据的同一 nic。 只有在对同一 nic。 以前的还原操作完成后，协议边缘将启动 NIC 在运行时数据还原操作 但是，协议边缘可能启动还原操作的 nic，另一个还原操作正在进行另一个 nic 时 因此，我们强烈建议扩展以非交错的方式执行还原操作。 例如，扩展应假定新的还原操作无法启动另一个 NIC 上之前正在进行的还原操作已完成的不同 nic。

 

有关此 OID 请求的详细信息，请参阅[还原的 HYPER-V 可扩展交换机运行时数据](restoring-hyper-v-extensible-switch-run-time-data.md)。

 

 





