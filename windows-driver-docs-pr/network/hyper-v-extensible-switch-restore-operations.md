---
title: Hyper-V 可扩展交换机还原操作
description: Hyper-V 可扩展交换机还原操作
ms.assetid: 283D9E43-79F2-47B1-8D29-39A8E7CBE2C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd0cc1665a2b10e8b90442db2b53e5e90ad1ce7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823836"
---
# <a name="hyper-v-extensible-switch-restore-operations"></a>Hyper-V 可扩展交换机还原操作


当 Hyper-v 子分区在停止或实时迁移后重新启动时，将还原该分区的运行时状态。 在还原操作过程中，Hyper-v 可扩展交换机扩展驱动程序可以还原有关可扩展交换机网络适配器（NIC）的运行时数据。

在 Hyper-v 子分区上执行还原操作时，可扩展交换机接口会向可扩展交换机的协议边缘发出信号，以便[\_交换机\_NIC\_restore](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)发出 OID 的 oid 集请求。 \_oid 的[**ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 NDIS\_交换机的**INFORMATIONBUFFER**成员\_nic\_RESTORE 请求包含指向[**NDIS\_switch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)\_\_\_状态结构的指针的指针。

当它处理此 OID 请求时，扩展会恢复网络适配器的运行时数据。 之前，此运行时数据是通过 oid [\_switch\_nic\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)和 OID\_交换机\_\_\_

当接收到[OID\_交换机\_NIC\_RESTORE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)请求时，可扩展交换机扩展必须首先确定它是否拥有运行时数据。 驱动程序通过比较\_\_NIC 的 NDIS 的**ExtensionId**成员的值来实现此功能， [ **\_将\_状态结构保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)到驱动程序用于标识自身的 GUID 值。

如果扩展插件拥有运行时数据，则将按以下方式还原这些数据：

1.  该扩展将**SaveData**成员中的运行时数据复制到驱动程序分配的存储。

    **请注意**  NDIS\_交换机的**PortId**成员的值[ **\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构可能与保存运行时数据时的**PortId**值不同。 如果在实时迁移从一台主机到另一台主机时保存了运行时数据，则会发生这种情况。 但是，可扩展交换机 NIC 的配置会在实时迁移时保留。 这使该扩展可以使用新的**PortId**值将运行时数据还原到可扩展交换机 NIC。

     

2.  扩展完成 OID 集请求，其 NDIS\_状态\_成功。

如果扩展不拥有运行时数据，则必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 方法请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展交换机 NIC 的运行时数据的还原操作完成后发出此 OID。

此 OID 请求通知扩展：还原操作仅对指定的可扩展交换机 NIC 完成。

有关此 OID 请求的详细信息，请参阅[oid\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)。

在运行时数据的还原操作过程中，可扩展交换机的协议边缘[\_交换机\_nic](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)上发出 oid 请求\_还原和[OID\_交换机\_nic\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)为 hyper-v 子分区连接的网络接口完成\_还原。 如果还原了多个 Hyper-v 子分区，则协议边缘\_\_NIC\_交换机 NIC 上发出不同的 OID 集\_交换机\_NIC\_RESTORE\_每个网络接口连接的完整请求。

**请注意**  可扩展交换机的协议边缘不会为同一 NIC 的运行时数据交错执行还原操作。 仅当上一次还原操作在同一 NIC 上完成后，协议边缘才会为 NIC 启动运行时数据还原操作。 但是，当另一个 NIC 正在进行另一个还原操作时，协议边缘可以为 NIC 启动还原操作。 因此，我们强烈建议扩展以非交错方式执行还原操作。 例如，扩展不应假定在针对其他 NIC 执行正在进行的还原操作之前，新的还原操作无法在另一个 NIC 上启动。

 

有关此 OID 请求的详细信息，请参阅[还原 Hyper-v 可扩展交换机运行时数据](restoring-hyper-v-extensible-switch-run-time-data.md)。

 

 





