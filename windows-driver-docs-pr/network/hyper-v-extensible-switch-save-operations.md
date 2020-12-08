---
title: Hyper-V 可扩展交换机保存操作
description: Hyper-V 可扩展交换机保存操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a8117bb76b45e6e93701a71ab0442fe77719fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836775"
---
# <a name="hyper-v-extensible-switch-save-operations"></a>Hyper-V 可扩展交换机保存操作


当 Hyper-v 子分区停止、保存或实时迁移时，将保存该分区的运行时状态。 在保存操作期间，Hyper-v 可扩展交换机扩展可以保存有关可扩展交换机网络适配器的运行时数据 (NIC) 。

在 Hyper-v 子分区上执行保存操作时，可扩展交换机接口会通知扩展操作。 将通过以下对象标识符向扩展通知 (OID) 请求：

<a href="" id="oid-switch-nic-save"></a>[OID \_ 交换机 \_ NIC \_ 保存](./oid-switch-nic-save.md)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展交换机 NIC 的保存操作期间发出此 OID。 它在处理此 OID 请求时，将返回 NIC 的运行时数据。 保存运行时数据后，它将通过 oid [ \_ 交换机 \_ NIC \_ 还原](./oid-switch-nic-restore.md)的 oid 设置请求进行还原。

接收到 [OID \_ 交换机 \_ NIC \_ SAVE](./oid-switch-nic-save.md) 方法请求时，扩展可以执行以下操作之一：

-   如果扩展具有要保存的运行时数据，则它会初始化 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构，并设置各个成员（例如 **ExtensionId** 成员），以标识自身及其要保存的数据。 该扩展还会将数据保存在 **ndis \_ 交换机 \_ NIC \_ 保存 \_ 状态** 结构内，从结构的开头开始 SaveDataOffset 字节，然后完成 OID 方法请求并使 NDIS \_ 状态 \_ 成功。

-   如果 [**ndis \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构没有提供足够的缓冲区大小（在 NDIS \_ 对象 \_ 标头 **大小** 成员中枚举以保存运行时状态），则扩展会将方法结构的 *BytesNeeded* 字段设置为 ndis \_ SIZEOF \_ ndis \_ SWITCH \_ NIC \_ 保存 \_ 状态 \_ 修订 \_ 1，并将保存数据所需的缓冲区量设置为，并使用 NDIS 状态缓冲区完成 OID \_ \_ \_ 太 \_ 短。 将重新颁发具有所需大小的 OID。
-   如果扩展没有要保存的运行时数据，则必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 方法请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关此 OID 请求的详细信息，请参阅 [处理 oid \_ 交换机 \_ NIC \_ SAVE 请求](./managing-hyper-v-extensible-switch-run-time-data.md)。

<a href="" id="oid-switch-nic-save-complete"></a>[OID \_ 交换机 \_ NIC \_ 保存 \_ 完毕](./oid-switch-nic-save.md)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展交换机 NIC 的运行时数据完成保存操作时发出此 OID。

此 OID 请求通知扩展：保存操作仅针对指定的可扩展交换机 NIC 完成。

有关此 OID 请求的详细信息，请参阅 [处理 oid \_ 交换机 \_ NIC \_ SAVE \_ COMPLETE 请求](./managing-hyper-v-extensible-switch-run-time-data.md)。

在保存运行时数据的操作期间，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ save](./oid-switch-nic-save.md) 和 oid 交换机 Nic 的 oid 请求 \_ \_ \_ \_ 。 hyper-v 子分区的网络接口已连接完成。 如果多个 Hyper-v 子分区停止或实时迁移，则协议边缘会发出不同的 OID \_ 交换机 \_ nic \_ save 和 OID \_ 交换机 nic， \_ \_ \_ 为每个网络接口连接保存完整请求。

**注意**  可扩展交换机的协议边缘不会为同一 NIC 的运行时数据交错保存操作。 只有在同一 NIC 上完成了上一个保存操作后，协议边缘才会为 NIC 启动运行时数据保存操作。 但是，如果另一个 NIC 正在进行另一个保存操作，协议边缘可能会为 NIC 启动保存操作。 因此，我们强烈建议扩展以非交错方式执行保存操作。 例如，扩展不应假定新的 save 操作无法在另一个 NIC 上启动，然后才能在其他 NIC 上完成正在进行的保存操作。

 

 

