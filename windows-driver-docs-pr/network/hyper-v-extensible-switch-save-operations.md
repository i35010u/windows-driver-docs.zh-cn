---
title: Hyper-V 可扩展交换机保存操作
description: Hyper-V 可扩展交换机保存操作
ms.assetid: 7148B094-2551-4035-A6BE-141DD01BEA14
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b480581ad55b75f0b9ae6f37cd989e132aabd6d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386540"
---
# <a name="hyper-v-extensible-switch-save-operations"></a>Hyper-V 可扩展交换机保存操作


当 HYPER-V 子分区已停止、 已保存，或实时迁移时，保存该分区的运行时状态。 在保存操作，HYPER-V 可扩展交换机扩展可以保存有关可扩展交换机网络适配器 (NIC) 的运行时数据。

保存时正在执行操作上的 HYPER-V 子分区，可扩展交换机接口通知有关操作的扩展。 通过以下对象标识符 (OID) 请求通知扩展：

<a href="" id="oid-switch-nic-save"></a>[OID\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)  
可扩展交换机接口指示在保存期间发出此 OID 的可扩展交换机的协议边缘操作可扩展的交换机 nic。 它处理此 OID 请求，该扩展返回运行时数据 nic。 运行时数据将保存之后，它通过 OID 的集请求还原[OID\_交换机\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)。

当它收到[OID\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)方法请求，该扩展可以执行以下项之一：

-   如果扩展具有要保存的运行时数据，则会初始化[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构并设置各种成员，如**ExtensionId**成员，若要标识本身和它正在保存数据。 扩展还节省了中的数据**NDIS\_交换机\_NIC\_保存\_状态**结构从结构开始的起始 SaveDataOffset 字节，然后完成OID 方法请求使用 NDIS\_状态\_成功。

-   如果[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构不提供足够的缓冲区大小，NDIS中枚举\_对象\_标头**大小**成员以保存运行时状态，该扩展设置方法结构*BytesNeeded*字段到 NDIS\_SIZEOF\_NDIS\_交换机\_NIC\_保存\_状态\_修订\_1 加上保存在保存所需的缓冲区的数据，并完成用 NDIS OID\_状态\_缓冲区\_过\_短。 使用所需的大小，将重新颁发 OID。
-   如果该扩展没有要保存的运行时数据，它必须调用[ **NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)。 这 OID 方法将请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

有关此 OID 请求的详细信息，请参阅[处理 OID\_交换机\_NIC\_保存请求](handling-the-oid-switch-nic-save-request.md)。

<a href="" id="oid-switch-nic-save-complete"></a>[OID\_交换机\_NIC\_保存\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)  
可扩展交换机接口发出信号发出在保存完成时此 OID 的可扩展交换机的协议边缘操作的运行时数据的可扩展的交换机 nic。

此 OID 请求向扩展通知的保存操作已完成仅对指定可扩展交换机 nic。

有关此 OID 请求的详细信息，请参阅[处理 OID\_交换机\_NIC\_保存\_完整的请求](handling-the-oid-switch-nic-save-complete-request.md)。

在保存运行时数据的操作，可扩展交换机的协议边缘发出的 OID 请求[OID\_切换\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)和 OID\_切换\_NIC\_保存\_完成连接 HYPER-V 子分区的网络接口。 如果多个 HYPER-V 子分区是已停止或实时迁移，协议边缘问题分隔集 OID\_交换机\_NIC\_保存和 OID\_交换机\_NIC\_保存\_完成请求的每个网络接口连接。

**请注意**  可扩展交换机的协议边缘会交替执行保存操作的运行时数据的同一 nic。 协议边缘将启动保存操作 NIC 的运行时数据才以前保存操作已完成在同一 nic。 但是，协议边缘可能会启动一个保存 nic 时保存操作的另一个操作正在进行的另一个 nic。 因此，我们强烈建议扩展执行保存操作以非交错的方式。 例如，扩展应假定，新的保存操作无法启动另一个 NIC 上之前持续保存操作已完成的不同 nic。

 

 

 





