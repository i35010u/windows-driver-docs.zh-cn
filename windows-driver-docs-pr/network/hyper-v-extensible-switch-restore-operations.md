---
title: Hyper-V 可扩展交换机还原操作
description: Hyper-V 可扩展交换机还原操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9512fca2dfee942832ee012224b4a565b155b6f2
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248175"
---
# <a name="hyper-v-extensible-switch-restore-operations"></a>Hyper-V 可扩展交换机还原操作


当 Hyper-v 子分区在停止或实时迁移后重新启动时，将还原该分区的运行时状态。 在还原操作过程中，Hyper-v 可扩展交换机扩展驱动程序可以还原有关可扩展交换机网络适配器 (NIC) 的运行时数据。

在 Hyper-v 子分区上执行还原操作时，可扩展交换机接口会向可扩展交换机的协议边缘发出信号，以发出 oid [ \_ 交换机 \_ NIC \_ 还原](./oid-switch-nic-save.md)的 oid 集请求。 OID 交换机 nic RESTORE 请求的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员 \_ \_ \_ 包含指向 [**NDIS \_ 交换机 \_ nic \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。

当它处理此 OID 请求时，扩展会恢复网络适配器的运行时数据。 此运行时数据以前是通过 oid [ \_ 交换机 \_ NIC \_ save](./oid-switch-nic-save.md) 和 oid \_ 交换机 \_ nic \_ save 完成的 oid 请求保存的 \_ 。

当它收到 [OID \_ 交换机 \_ NIC \_ RESTORE](./oid-switch-nic-restore.md) 请求时，可扩展交换机扩展必须首先确定它是否拥有运行时数据。 驱动程序通过将 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **ExtensionId** 成员的值与驱动程序用于标识自身的 GUID 值进行比较来实现此功能。

如果扩展插件拥有运行时数据，则将按以下方式还原这些数据：

1.  该扩展将 **SaveData** 成员中的运行时数据复制到驱动程序分配的存储。

    **注意** [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **PortId** 成员的值可能与保存运行时数据时的 **PortId** 值不同。 如果在实时迁移从一台主机到另一台主机时保存了运行时数据，则会发生这种情况。 但是，可扩展交换机 NIC 的配置会在实时迁移时保留。 这使该扩展可以使用新的 **PortId** 值将运行时数据还原到可扩展交换机 NIC。

     

2.  扩展完成 OID 集请求，NDIS 状态为 \_ " \_ 成功"。

如果扩展不拥有运行时数据，则必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 方法请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID \_ 交换机 \_ NIC \_ 还原 \_ 完成](./oid-switch-nic-restore-complete.md)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展交换机 NIC 的运行时数据的还原操作完成后发出此 OID。

此 OID 请求通知扩展：还原操作仅对指定的可扩展交换机 NIC 完成。

有关此 OID 请求的详细信息，请参阅 [OID \_ 交换机 \_ NIC \_ 还原 \_ 完成](./oid-switch-nic-restore-complete.md)。

在运行时数据的还原操作过程中，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ Nic \_ restore](./oid-switch-nic-restore.md) 和 [oid \_ 交换机 \_ Nic \_ 还原 \_ ](./oid-switch-nic-restore-complete.md) 的 oid 请求已完成，hyper-v 子分区的网络接口已连接。 如果还原多个 Hyper-v 子分区，则协议边缘会发出不同的 OID \_ 交换机 \_ nic \_ restore 和 oid \_ 交换机 \_ nic \_ 还原 \_ 对每个网络接口连接的完整请求。

**注意**  可扩展交换机的协议边缘不会为同一 NIC 的运行时数据交错执行还原操作。 仅当上一次还原操作在同一 NIC 上完成后，协议边缘才会为 NIC 启动运行时数据还原操作。 但是，当另一个 NIC 正在进行另一个还原操作时，协议边缘可以为 NIC 启动还原操作。 因此，我们强烈建议扩展以非交错方式执行还原操作。 例如，扩展不应假定在针对其他 NIC 执行正在进行的还原操作之前，新的还原操作无法在另一个 NIC 上启动。

 

有关此 OID 请求的详细信息，请参阅 [还原 Hyper-v 可扩展交换机 Run-Time 数据](./managing-hyper-v-extensible-switch-run-time-data.md)。

 

