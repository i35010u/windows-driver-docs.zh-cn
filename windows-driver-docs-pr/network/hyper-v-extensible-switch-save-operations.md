---
title: Hyper-V 可扩展交换机保存操作
description: Hyper-V 可扩展交换机保存操作
ms.assetid: 7148B094-2551-4035-A6BE-141DD01BEA14
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92171a843685c950d157fe3472741fdd273a8a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823829"
---
# <a name="hyper-v-extensible-switch-save-operations"></a>Hyper-V 可扩展交换机保存操作


当 Hyper-v 子分区停止、保存或实时迁移时，将保存该分区的运行时状态。 在保存操作期间，Hyper-v 可扩展交换机扩展可以保存有关可扩展交换机网络适配器（NIC）的运行时数据。

在 Hyper-v 子分区上执行保存操作时，可扩展交换机接口会通知扩展操作。 将通过以下对象标识符（OID）请求通知扩展：

<a href="" id="oid-switch-nic-save"></a>[OID\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展交换机 NIC 的保存操作期间发出此 OID。 它在处理此 OID 请求时，将返回 NIC 的运行时数据。 保存运行时数据后，将通过 oid [\_交换机\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)将其还原。

当接收到[OID\_交换机\_NIC\_SAVE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)方法请求时，扩展可以执行下列操作之一：

-   如果扩展具有要保存的运行时数据，则它会初始化[**NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构，并设置各个成员（例如**ExtensionId**成员），以标识自身及其数据保存. 该扩展还会将 Ndis\_交换机中的数据保存 **\_NIC\_SAVE\_状态**结构，从结构的开头开始 SaveDataOffset 字节，然后通过 NDIS\_状态完成 OID 方法请求\_成功。

-   如果[**ndis\_交换机\_NIC\_SAVE\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构没有提供足够的缓冲区大小，在 NDIS\_对象\_标头**大小**成员中枚举以保存运行时状态，扩展会将方法结构的*BytesNeeded*字段设置为 NDIS\_SIZEOF\_NDIS\_交换机\_NIC\_将\_状态\_1 加上保存所需的缓冲区数量保存数据，并通过 NDIS\_状态\_缓冲区来完成 OID，\_\_太短。 将重新颁发具有所需大小的 OID。
-   如果扩展没有要保存的运行时数据，则必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 方法请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关此 OID 请求的详细信息，请参阅[处理 oid\_交换机\_NIC\_保存请求](handling-the-oid-switch-nic-save-request.md)。

<a href="" id="oid-switch-nic-save-complete"></a>[OID\_交换机\_NIC\_保存\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展交换机 NIC 的运行时数据完成保存操作时发出此 OID。

此 OID 请求通知扩展：保存操作仅针对指定的可扩展交换机 NIC 完成。

有关此 OID 请求的详细信息，请参阅[处理 oid\_交换机\_NIC\_保存\_完成请求](handling-the-oid-switch-nic-save-complete-request.md)。

在保存运行时数据的操作期间，可扩展交换机的协议边缘[\_交换机\_nic](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)上发出 oid 请求\_SAVE 和 OID\_SWITCH\_nic\_为网络完成保存\_Hyper-v 子分区的接口已连接。 如果已停止或实时迁移多个 Hyper-v 子分区，则协议边缘会发出不同的 OID 集\_交换机\_NIC\_SAVE 和 OID\_交换机\_NIC\_保存每个网络的\_完成请求接口连接。

**请注意**  可扩展交换机的协议边缘不会交错保存同一 NIC 的运行时数据的操作。 只有在同一 NIC 上完成了上一个保存操作后，协议边缘才会为 NIC 启动运行时数据保存操作。 但是，如果另一个 NIC 正在进行另一个保存操作，协议边缘可能会为 NIC 启动保存操作。 因此，我们强烈建议扩展以非交错方式执行保存操作。 例如，扩展不应假定新的 save 操作无法在另一个 NIC 上启动，然后才能在其他 NIC 上完成正在进行的保存操作。

 

 

 





