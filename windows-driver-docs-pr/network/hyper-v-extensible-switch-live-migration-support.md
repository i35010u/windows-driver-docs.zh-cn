---
title: Hyper-V 可扩展交换机实时迁移支持
description: Hyper-V 可扩展交换机实时迁移支持
ms.assetid: 4AFC9E3F-C9C5-4693-BA8C-BC7122A4055F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39dcc24ec24720d1603d8073edc91642c26950df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823883"
---
# <a name="hyper-v-extensible-switch-live-migration-support"></a>Hyper-V 可扩展交换机实时迁移支持


在 Hyper-v 实时迁移过程中，子分区或*虚拟机（VM）* 在一台主机（*源主机*）上停止，并迁移到另一台主计算机（*目标主机*）。 在实时迁移期间，会发生以下操作：

-   当源主机上启动实时迁移时，可扩展交换机接口请求基础扩展来保存每个端口及其关联网络适配器连接的运行时数据。

    有关此操作的详细信息，请参阅[Hyper-v 可扩展交换机保存操作](hyper-v-extensible-switch-save-operations.md)。

-   在目标主机上完成实时迁移之前，可扩展交换机接口请求基础扩展以还原每个端口及其关联网络适配器连接的运行时数据。

    有关此操作的详细信息，请参阅[Hyper-v 可扩展交换机还原操作](hyper-v-extensible-switch-restore-operations.md)。

在实时迁移的设置阶段，源主机与目标物理主机建立 TCP 连接。 Hyper-v 通过此连接将源 VM 的配置数据传输到目标物理主机。 在目标主机上设置主干 VM，并将内存分配给目标 VM。 此时，Hyper-v 会将源 VM 的状态（包括其内存页）传输到目标 VM。

可扩展交换机接口还使用 TCP 连接在实时迁移期间同步步骤和结果。 例如，在目标主机上运行的接口请求传输源主机中与已迁移 VM 关联的端口和网络适配器连接的运行时数据。

在目标 VM 在目标主机上联机之前，可扩展交换机接口将执行以下步骤：

1.  验证端口是通过 Oid 的对象标识符（OID）设置请求（ [\_SWITCH\_端口\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)）在目标主机上创建的。 如果成功创建端口，则可扩展交换机接口会发出其他 OID 请求，以通过基础扩展来验证端口策略的属性。

    如果扩展无法创建端口或使任何策略属性无效，则不会继续对该目标节点和交换机执行实时迁移。

    有关验证端口及其用法的详细信息，请参阅[验证端口](validation-ports.md)。

2.  策略属性验证成功完成后，将通过 oid [\_SWITCH\_端口\_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)在目标主机上删除验证端口。 删除此端口后，会在目标主机上创建一个操作端口，并在其位置创建一个操作端口。 [**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构与[OID\_切换\_端口\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)为操作端口创建请求包含与用于创建端口的数据相同的数据源主机。

    如果成功创建了操作端口，则会将端口策略添加到操作端口。

3.  如果设置成功地应用于目标主机上的操作端口，则会为源主机上的操作端口发出保存操作。

4.  如果保存操作已成功完成，则将按以下方式在源主机上删除操作端口及其网络适配器连接：

    1.  首先，通过 oid [\_交换机\_NIC\_断开](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)连接来断开网络连接。 完成此 OID 请求后，源主机上的网络适配器连接将通过 oid [\_SWITCH\_NIC\_删除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)来删除。

    2.  删除网络适配器连接后，将通过 oid [\_交换机\_端口\_拆卸](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)来细分操作端口。 完成此 OID 请求后，将通过 oid\_SWITCH\_端口\_DELETE 来删除操作端口。

5.  为目标主机上的操作端口创建了一个网络适配器连接，该连接通过 oid [\_交换机\_NIC\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)来创建。 如果此 OID 请求成功完成，则将通过 oid [\_交换机\_NIC\_连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)的 oid 集请求在关联的操作端口上建立网络适配器连接。

    如果成功建立网络适配器连接，则会在目标主机上还原操作端口和网络适配器连接的运行时数据。

    此时，基础扩展可以在网络适配器连接上执行资源保留和验证。

 

 





