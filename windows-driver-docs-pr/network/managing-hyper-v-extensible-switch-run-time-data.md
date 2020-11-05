---
title: 管理 Hyper-V 可扩展交换机运行时数据
description: 管理 Hyper-V 可扩展交换机运行时数据
ms.assetid: 08A353F5-D8CB-4645-9337-8169D302F6F2
ms.date: 12/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8010e00ec91e74d920fe56ac24bcec0f371e17df
ms.sourcegitcommit: 3464f10ffa0727e38fbe225cfab52bb8c2bb1747
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93352996"
---
# <a name="managing-hyper-v-extensible-switch-run-time-data"></a>管理 Hyper-V 可扩展交换机运行时数据

本主题介绍 Hyper-v 可扩展交换机扩展的保存和还原操作。 这些操作允许扩展为单独的可扩展交换机网络适配器（)  (Nic 保存和还原运行时数据。 当将网络适配器连接到可扩展交换机端口的 Hyper-v 子分区正在停止或启动时，将执行这些操作。

## <a name="saving-hyper-v-extensible-switch-run-time-data"></a>Run-Time 数据保存 Hyper-v 可扩展交换机

本节介绍 Hyper-v 可扩展交换机扩展可为单独的网络适配器（)  (Nic 保存运行时数据的操作。 当与可扩展交换机端口的网络适配器连接正在停止或正在保存其状态时，将执行此操作。

### <a name="handling-the-oid_switch_nic_save-request"></a>处理 OID \_ 交换机 \_ NIC \_ SAVE 请求

如果停止将网络适配器连接到可扩展交换机端口的 Hyper-v 子分区或其状态已保存，则会通知 Hyper-v 可扩展交换机接口。 这会导致可扩展交换机的协议边缘 (oid 发出对象标识符) oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-nic-save.md) 的方法请求在可扩展交换机驱动程序堆栈中按下。 当可扩展交换机扩展接收此 OID 请求时，它可以保存附加到子分区的指定网络适配器连接的运行时数据。

[OID \_ 交换机 \_ nic \_ save](./oid-switch-nic-save.md)请求的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ nic \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。 此结构由可扩展交换机的协议边缘分配，并按以下方式进行初始化：

-   **标头** 成员被初始化为包含当前类型，revisionof [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 Size 设置为完整的缓冲区大小。

-   **PortId** 成员包含要对其执行保存操作的可扩展交换机端口的唯一标识符。

接收到 [OID \_ 交换机 \_ NIC \_ SAVE](./oid-switch-nic-save.md) 方法请求时，扩展将执行以下操作：

1.  该扩展插件读取 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **PortId** 成员。

2.  如果扩展具有为指定 NIC 保存的运行时数据，则会将其数据保存在 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构内，从结构的开头开始 *SaveDataOffset* 字节。 然后，扩展将完成 OID 方法请求，并 \_ 成功执行 NDIS 状态 \_ 。

3.  如果 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构没有提供足够的缓冲区来保存运行时状态，扩展插件会将方法结构的 *BytesNeeded* 字段设置为 **ndis \_ SIZEOF \_ ndis \_ SWITCH \_ NIC \_ 保存 \_ 状态修订号 \_ \_ 1** 加上保存数据所需的缓冲区数量，并使用 **NDIS 状态缓冲区完成 OID \_ \_ \_ 太 \_ 短** 。 将用所需大小重新发出 OID。

4.  如果该扩展没有要为指定的 NIC 保存的运行时数据，则必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 方法请求转发到可扩展交换机驱动程序堆栈中的底层驱动程序。 有关此过程的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 OID 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

如果扩展具有要保存的运行时端口数据，则在 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构中保存运行时端口数据时，必须遵循以下准则：

1.  该扩展将 **ExtensionId** 成员设置为唯一标识该驱动程序的 GUID 值。
2.  该扩展将 **ExtensionFriendlyName** 成员设置为驱动程序的名称。

    **注意**  NDIS \_ 交换机 \_ 扩展 \_ FRIENDLYNAME 数据类型由 [**IF \_ 计数 \_ 字符串**](/windows/win32/api/ifdef/ns-ifdef-if_counted_string_lh) 结构的类型定义。 此结构定义的字符串不必以 null 结尾。 但是，字符串的长度必须设置为此结构的 **长度** 成员。 如果字符串以 NULL 结尾，则 **长度** 成员不能包含终止 NULL 字符。     

3.  如果功能类与保存的运行时数据相关联，则扩展将使用唯一标识类的 GUID 来设置 **FeatureClassId** 。

    **注意**  如果某个功能类未与保存的运行时数据相关联，则该扩展将 **FeatureClassId** 设置为零。     

4.  该扩展将运行时数据复制到 **SaveData** 成员，并将 **SaveDataSize** 成员设置为运行时数据的大小（以字节为单位）。

**注意** 此扩展不能更改 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **标头** 或 **PortId** 成员。 

[Oid \_ 交换机 \_ NIC \_ SAVE](./oid-switch-nic-save.md)的 oid 方法请求最终由可扩展交换机的基础微型端口边缘处理。 通过可扩展交换机驱动程序堆栈将此 OID 方法请求转发到微型端口驱动程序后，微型端口驱动程序将完成 OID 请求，并提供 NDIS \_ 状态 \_ SUCCESS。 这会通知可扩展交换机的协议边缘已查询了运行时端口数据的可扩展交换机驱动程序堆栈中的所有扩展。 然后，可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ save \_ 完成](./oid-switch-nic-save-complete.md) 的 oid 集请求，以完成保存操作。

### <a name="handling-the-oid_switch_nic_save_complete-request"></a>处理 OID \_ 交换机 \_ NIC \_ SAVE \_ COMPLETE 请求

如果已暂停与可扩展交换机端口建立网络适配器连接的 Hyper-v 子分区或正在保存其状态，则会通知 Hyper-v 可扩展交换机接口。 这会导致可扩展交换机的协议边缘 (oid 发出对象标识符) oid [ \_ 交换机 \_ NIC \_ ](./oid-switch-nic-save.md) 的方法请求在可扩展交换机驱动程序堆栈中按下。

当每个 Hyper-v 可扩展交换机扩展保存其运行时数据时，可扩展交换机的协议边缘会通知基础扩展保存操作已完成。 协议边缘通过发出 oid [ \_ 交换机 \_ NIC \_ \_ ](./oid-switch-nic-save-complete.md) 的 oid 集请求来实现此功能。

**注意**  为可扩展交换机网络适配器连接启动运行时保存操作时，将不会执行相同网络适配器连接的另一个保存操作，直到发出 [OID \_ 交换机 \_ NIC \_ save \_ COMPLETE](./oid-switch-nic-save-complete.md) 请求。 但在此期间，可能会发生其他网络适配器连接的保存操作。 

[OID \_ 交换机 \_ nic \_ Save \_ COMPLETE](./oid-switch-nic-save-complete.md)请求的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ nic \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。 此结构由可扩展交换机的协议边缘分配。

当它收到 oid [ \_ 交换机 \_ NIC \_ SAVE \_ 完成](./oid-switch-nic-save-complete.md)的 oid 设置请求时，扩展必须遵循以下准则：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构。

-   扩展必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以通过可扩展交换机扩展堆栈转发此 OID 请求。 此扩展不能使 OID 请求失败。

    **注意**  扩展应监视此 OID 请求的完成状态。 此扩展将执行此操作以检测保存操作是否已成功完成。     

[Oid \_ 交换机 \_ NIC \_ SAVE \_ 完成](./oid-switch-nic-save-complete.md)的 oid 方法请求最终由可扩展交换机的基础微型端口边缘处理。 小型端口边缘收到此 OID 方法请求后，它将完成具有 NDIS 状态成功的 OID 请求 \_ \_ 。 这会通知可扩展交换机的协议边缘：可扩展交换机驱动程序堆栈中的所有扩展都已完成保存操作。

## <a name="restoring-hyper-v-extensible-switch-run-time-data"></a>Run-Time 数据还原 Hyper-v 可扩展交换机

在从暂停中恢复与可扩展交换机端口建立网络适配器连接的 Hyper-v 子分区时，会通知 Hyper-v 可扩展交换机接口。 这会导致可扩展交换机的协议边缘 (OID 发出对象标识符) 在可扩展交换机驱动程序堆栈中关闭 [oid \_ 交换机 \_ NIC \_ 还原](./oid-switch-nic-restore.md) 的请求。 当扩展插件收到此 OID 请求时，它可以为子分区使用的可扩展交换机端口还原其运行时数据。

[OID \_ 交换机 \_ nic \_ RESTORE](./oid-switch-nic-save.md)请求的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ nic \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。 此结构由可扩展交换机的协议边缘分配。

当其收到 oid [ \_ 交换机 \_ NIC \_ 还原](./oid-switch-nic-restore.md)的 oid 集请求时，可扩展交换机扩展必须首先确定它是否拥有运行时数据。 此扩展通过将 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **ExtensionId** 成员的值与扩展用于标识自身的 GUID 值进行比较来实现此功能。

如果扩展插件拥有可扩展交换机 NIC 的运行时数据，则将按以下方式还原这些数据：

1.  该扩展将 **SaveData** 成员中的运行时数据复制到驱动程序分配的存储。

    **注意** [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **PortId** 成员的值可能与保存运行时数据时的 **PortId** 值不同。 如果在实时迁移从一台主机到另一台主机时保存了运行时数据，则会发生这种情况。 但是，可扩展交换机 NIC 的配置会在实时迁移时保留。 这使该扩展可以使用新的 **PortId** 值将运行时数据还原到可扩展交换机 NIC。     

2.  扩展完成 OID 集请求，NDIS 状态为 \_ " \_ 成功"。

如果扩展不拥有要保存的指定运行时数据，则扩展将调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)。 这会将 OID 集请求转发到可扩展交换机驱动程序堆栈中的底层驱动程序。 在这种情况下，扩展不能修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构。 有关如何转发 OID 请求的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 Oid 请求](filtering-oid-requests-in-an-ndis-filter-driver.md)。

如果 oid [ \_ 交换机 \_ NIC \_ 还原](./oid-switch-nic-restore.md) 的 oid 设置请求已完成，并且 NDIS \_ 状态为 \_ 成功，则可扩展交换机的协议边缘会颁发另一个 OID 设置请求。 当它收到这个新的 OID 集请求时，扩展可以执行下列操作之一：

-   如果它拥有新 OID 请求中的运行时数据，则该扩展将在 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构中还原其他运行时数据。 然后，扩展将完成 OID 请求，并 \_ 成功执行 NDIS 状态 \_ 。

-   如果它不拥有新 OID 请求中的运行时数据，则扩展将调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将此 OID 集请求转发到底层驱动程序。

<a href="" id="oid-switch-nic-restore-complete"></a>[OID \_ 交换机 \_ NIC \_ 还原 \_ 完成](./oid-switch-nic-restore-complete.md)  
可扩展交换机接口向可扩展交换机的协议边缘发出信号，以便在可扩展 switchnetwork 适配器的运行时数据的还原操作完成后发出此 OID。

此 OID 请求通知扩展：还原操作仅对指定的可扩展交换机 NIC 完成。

有关此 OID 请求的详细信息，请参阅 [OID \_ 交换机 \_ NIC \_ 还原 \_ 完成](./oid-switch-nic-restore-complete.md)。

**注意**  如果 [OID \_ 交换机 \_ NIC \_ 还原](./oid-switch-nic-restore.md) 集请求由可扩展交换机的微型端口边缘接收，则它将完成具有 NDIS 状态成功的 oid \_ 请求 \_ 。 这会通知可扩展交换机的协议边缘，其中没有扩展拥有运行时数据。 如果发生这种情况，可扩展交换机接口会记录一个事件，该事件记录最初保存运行时端口数据的扩展的 **ExtensionId** 和 **PortId** 成员值。