---
title: 管理 Hyper-v 可扩展交换机运行时数据
description: 管理 Hyper-v 可扩展交换机运行时数据
ms.assetid: 08A353F5-D8CB-4645-9337-8169D302F6F2
ms.date: 12/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: b52fdc73bcaeb16b2ddd51296d5a18d3a9c6de70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844120"
---
# <a name="managing-hyper-v-extensible-switch-run-time-data"></a>管理 Hyper-v 可扩展交换机运行时数据

本主题介绍 Hyper-v 可扩展交换机扩展的保存和还原操作。 这些操作允许扩展插件保存和还原单个可扩展交换机网络适配器（Nic）的运行时数据。 当将网络适配器连接到可扩展交换机端口的 Hyper-v 子分区正在停止或启动时，将执行这些操作。

## <a name="saving-hyper-v-extensible-switch-run-time-data"></a>保存 Hyper-v 可扩展交换机运行时数据

本节介绍 Hyper-v 可扩展交换机扩展可为单个网络适配器（Nic）保存运行时数据的操作。 当与可扩展交换机端口的网络适配器连接正在停止或正在保存其状态时，将执行此操作。

### <a name="handling-the-oid_switch_nic_save-request"></a>处理 OID\_交换机\_NIC\_保存请求

如果停止将网络适配器连接到可扩展交换机端口的 Hyper-v 子分区或其状态已保存，则会通知 Hyper-v 可扩展交换机接口。 这会导致可扩展交换机的协议边缘发出 OID 的对象标识符（OID）方法请求[\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)可扩展交换机驱动程序堆栈。 当可扩展交换机扩展接收此 OID 请求时，它可以保存附加到子分区的指定网络适配器连接的运行时数据。

\_oid 的[**ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 NDIS\_交换机的**INFORMATIONBUFFER**成员[\_nic\_SAVE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)请求包含指向[**NDIS\_交换机\_nic 的指针\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 此结构由可扩展交换机的协议边缘分配，并按以下方式进行初始化：

-   **标头**成员被初始化为包含当前类型，revisionof [**NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 Size 设置为完整的缓冲区大小。

-   **PortId**成员包含要对其执行保存操作的可扩展交换机端口的唯一标识符。

当接收到[OID\_交换机\_NIC\_SAVE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)方法请求时，扩展将执行以下操作：

1.  该扩展读取\_交换机\_NIC 的**PortId**成员， [ **\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。

2.  如果扩展具有为指定 NIC 保存的运行时数据，则它会将其数据保存在[**NDIS\_交换机\_NIC\_保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)从结构开始开始*SaveDataOffset*字节开始的\_状态结构。 然后，扩展完成 OID 方法请求，并将 NDIS\_状态\_SUCCESS。

3.  如果[**NDIS\_交换机\_NIC\_SAVE\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构没有提供足够的缓冲区来保存运行时状态，扩展会将方法结构的*BytesNeeded*字段设置为**NDIS\_SIZEOF\_NDIS\_交换机\_NIC\_保存\_状态\_1**加上保存数据所需的缓冲区量，并通过**NDIS\_状态\_缓冲区来完成 OID\_太小了\_** 。\_ 将用所需大小重新发出 OID。

4.  如果该扩展没有要为指定的 NIC 保存的运行时数据，则必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 方法请求转发到可扩展交换机驱动程序堆栈中的底层驱动程序。 有关此过程的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

如果扩展插件具有要保存的运行时端口数据，则在\_交换机\_NIC 中保存运行时端口数据时，必须遵循以下指导原则[ **\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构：

1.  该扩展将**ExtensionId**成员设置为唯一标识该驱动程序的 GUID 值。
2.  该扩展将**ExtensionFriendlyName**成员设置为驱动程序的名称。

    **请注意**  NDIS\_交换机\_扩展\_FRIENDLYNAME 数据类型由定义（[**如果\_的字符串**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_if_counted_string_lh)结构进行计数）。\_ 此结构定义的字符串不必以 null 结尾。 但是，字符串的长度必须设置为此结构的**长度**成员。 如果字符串以 NULL 结尾，则**长度**成员不能包含终止 NULL 字符。     

3.  如果功能类与保存的运行时数据相关联，则扩展将使用唯一标识类的 GUID 来设置**FeatureClassId** 。

    **请注意**  如果某个功能类未与已保存的运行时数据相关联，则该扩展将**FeatureClassId**设置为零。     

4.  该扩展将运行时数据复制到**SaveData**成员，并将**SaveDataSize**成员设置为运行时数据的大小（以字节为单位）。

**请注意**  扩展不能更改 NDIS\_交换机的**标头**或**PORTID**成员[ **\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 

[Oid\_SWITCH\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)的 oid 方法请求最终由可扩展交换机的基础微型端口边缘处理。 通过可扩展交换机驱动程序堆栈将此 OID 方法请求转发到微型端口驱动程序后，微型端口驱动程序将使用 NDIS\_状态完成 OID 请求\_成功。 这会通知可扩展交换机的协议边缘已查询了运行时端口数据的可扩展交换机驱动程序堆栈中的所有扩展。 然后，可扩展交换机的协议边缘发出 oid\_交换机的 OID 集请求[\_NIC\_保存\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)来完成保存操作。

### <a name="handling-the-oid_switch_nic_save_complete-request"></a>处理 OID\_交换机\_NIC\_保存\_完成请求

如果已暂停与可扩展交换机端口建立网络适配器连接的 Hyper-v 子分区或正在保存其状态，则会通知 Hyper-v 可扩展交换机接口。 这会导致可扩展交换机的协议边缘发出 OID 的对象标识符（OID）方法请求[\_交换机\_NIC\_保存](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)可扩展交换机驱动程序堆栈。 有关此过程的详细信息，请参阅[处理 OID\_交换机\_NIC\_保存请求](handling-the-oid-switch-nic-save-request.md)。

当每个 Hyper-v 可扩展交换机扩展保存其运行时数据时，可扩展交换机的协议边缘会通知基础扩展保存操作已完成。 协议边缘执行此工作的方式是：\_NIC 发出 oid\_开关的 OID 集请求[\_保存\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)可扩展交换机驱动程序堆栈。

**请注意**  为可扩展交换机网络适配器连接启动运行时保存操作时，将不会执行相同网络适配器连接的另一个保存操作，直到[OID\_交换机\_NIC\_发出 SAVE\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)请求。 但在此期间，可能会发生其他网络适配器连接的保存操作。 

\_oid 的[**NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 NDIS\_交换机的**INFORMATIONBUFFER**成员[\_NIC\_SAVE\_COMPLETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)请求包含指向[**NDIS\_SWITCH 的指针\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 此结构由可扩展交换机的协议边缘分配。

当收到 oid\_SWITCH\_NIC 的 OID 集请求时[\_保存\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)，扩展必须遵循以下准则：

-   扩展不能修改[**NDIS\_交换机\_NIC\_保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)与 OID 请求关联\_状态结构。

-   扩展必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以通过可扩展交换机扩展堆栈转发此 OID 请求。 此扩展不能使 OID 请求失败。

    **请注意**  扩展应监视此 OID 请求的完成状态。 此扩展将执行此操作以检测保存操作是否已成功完成。     

[Oid\_交换机\_\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)的 oid 方法请求最终由可扩展交换机的基础微型端口边缘处理。 小型端口边缘收到此 OID 方法请求后，它将完成 OID 请求，并将 NDIS\_状态\_SUCCESS。 这会通知可扩展交换机的协议边缘：可扩展交换机驱动程序堆栈中的所有扩展都已完成保存操作。

## <a name="restoring-hyper-v-extensible-switch-run-time-data"></a>还原 Hyper-v 可扩展交换机运行时数据

在从暂停中恢复与可扩展交换机端口建立网络适配器连接的 Hyper-v 子分区时，会通知 Hyper-v 可扩展交换机接口。 这会导致可扩展交换机的协议边缘发出 OID 的对象标识符（OID）设置请求[\_交换机\_NIC\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)向下还原可扩展交换机驱动程序堆栈。 当扩展插件收到此 OID 请求时，它可以为子分区使用的可扩展交换机端口还原其运行时数据。

\_oid 的[**ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 NDIS\_交换机的**INFORMATIONBUFFER**成员[\_nic\_RESTORE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)请求包含指向[**NDIS\_交换机\_nic 的指针\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 此结构由可扩展交换机的协议边缘分配。

当它接收到 oid [\_SWITCH\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)时，可扩展交换机扩展必须首先确定它是否拥有运行时数据。 此扩展通过比较[ **\_\_NIC 的 NDIS 交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)的**ExtensionId**成员的值，\_将\_状态结构保存到扩展用于标识自身的 GUID 值。

如果扩展插件拥有可扩展交换机 NIC 的运行时数据，则将按以下方式还原这些数据：

1.  该扩展将**SaveData**成员中的运行时数据复制到驱动程序分配的存储。

    **请注意**  NDIS\_交换机的**PortId**成员的值[ **\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构可能与保存运行时数据时的**PortId**值不同。 如果在实时迁移从一台主机到另一台主机时保存了运行时数据，则会发生这种情况。 但是，可扩展交换机 NIC 的配置会在实时迁移时保留。 这使该扩展可以使用新的**PortId**值将运行时数据还原到可扩展交换机 NIC。     

2.  扩展完成 OID 集请求，其 NDIS\_状态\_成功。

如果扩展不拥有要保存的指定运行时数据，则扩展将调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 集请求转发到可扩展交换机驱动程序堆栈中的底层驱动程序。 在这种情况下，扩展不能修改[**NDIS\_交换机\_NIC\_保存**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)与 OID 请求关联\_状态结构。 有关如何转发 OID 请求的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

如果 oid 设置[oid\_交换机\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)已完成，并且 NDIS\_状态\_成功，则可扩展交换机的协议边缘会颁发另一个 OID 集请求。 当它收到这个新的 OID 集请求时，扩展可以执行下列操作之一：

-   如果它拥有新 OID 请求中的运行时数据，扩展将在[**NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构中还原其他运行时数据。 然后，扩展完成 OID 请求，并将 NDIS\_状态\_SUCCESS。

-   如果它不拥有新 OID 请求中的运行时数据，则扩展将调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将此 OID 集请求转发到底层驱动程序。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展 switchnetwork 适配器的运行时数据的还原操作完成后发出此 OID。

此 OID 请求通知扩展：还原操作仅对指定的可扩展交换机 NIC 完成。

有关此 OID 请求的详细信息，请参阅[oid\_交换机\_NIC\_还原\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore-complete)。

**请注意**  如果[oid\_交换机\_NIC\_还原](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)集请求是由可扩展交换机的微型端口边缘接收的，则它将使用 NDIS\_状态\_成功完成 oid 请求。 这会通知可扩展交换机的协议边缘，其中没有扩展拥有运行时数据。 如果发生这种情况，可扩展交换机接口会记录一个事件，该事件记录最初保存运行时端口数据的扩展的**ExtensionId**和**PortId**成员值。