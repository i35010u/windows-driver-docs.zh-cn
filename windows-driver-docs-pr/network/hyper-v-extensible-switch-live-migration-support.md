---
title: Hyper-V 可扩展交换机实时迁移支持
description: Hyper-V 可扩展交换机实时迁移支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4b2e496f8c025834f302a2bcf9619351aae8896
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821353"
---
# <a name="hyper-v-extensible-switch-live-migration-support"></a>Hyper-V 可扩展交换机实时迁移支持


在 Hyper-v 实时迁移过程中，子分区或 *虚拟机 (VM)* 在一台主机上被停止 (*源主机*) 并迁移到另一台主机 (*目标主机*) 。 在实时迁移期间，会发生以下操作：

-   当源主机上启动实时迁移时，可扩展交换机接口请求基础扩展来保存每个端口及其关联网络适配器连接的运行时数据。

    有关此操作的详细信息，请参阅 [Hyper-v 可扩展交换机保存操作](hyper-v-extensible-switch-save-operations.md)。

-   在目标主机上完成实时迁移之前，可扩展交换机接口请求基础扩展以还原每个端口及其关联网络适配器连接的运行时数据。

    有关此操作的详细信息，请参阅 [Hyper-v 可扩展交换机还原操作](hyper-v-extensible-switch-restore-operations.md)。

在实时迁移的设置阶段，源主机与目标物理主机建立 TCP 连接。 Hyper-v 通过此连接将源 VM 的配置数据传输到目标物理主机。 在目标主机上设置主干 VM，并将内存分配给目标 VM。 此时，Hyper-v 会将源 VM 的状态（包括其内存页）传输到目标 VM。

可扩展交换机接口还使用 TCP 连接在实时迁移期间同步步骤和结果。 例如，在目标主机上运行的接口请求传输源主机中与已迁移 VM 关联的端口和网络适配器连接的运行时数据。

在目标 VM 在目标主机上联机之前，可扩展交换机接口将执行以下步骤：

1.  验证端口通过对象标识符 (OID 在目标主机上创建，) 设置 [oid \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md)请求。 如果成功创建端口，则可扩展交换机接口会发出其他 OID 请求，以通过基础扩展来验证端口策略的属性。

    如果扩展无法创建端口或使任何策略属性无效，则不会继续对该目标节点和交换机执行实时迁移。

    有关验证端口及其用法的详细信息，请参阅 [验证端口](validation-ports.md)。

2.  策略属性验证成功完成后，将通过 oid [ \_ 交换机 \_ 端口 \_ 删除](./oid-switch-port-delete.md)的 oid 集请求在目标主机上删除验证端口。 删除此端口后，会在目标主机上创建一个操作端口，并在其位置创建一个操作端口。 与用于操作端口的 [OID \_ 交换机 \_ 端口 \_ 创建](./oid-switch-port-create.md)请求关联的 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构包含的数据与在源主机上创建端口时使用的数据相同。

    如果成功创建了操作端口，则会将端口策略添加到操作端口。

3.  如果设置成功地应用于目标主机上的操作端口，则会为源主机上的操作端口发出保存操作。

4.  如果保存操作已成功完成，则将按以下方式在源主机上删除操作端口及其网络适配器连接：

    1.  网络连接首先通过 oid [ \_ 交换机 \_ NIC \_ 断开连接](./oid-switch-nic-disconnect.md)的 oid 集请求断开连接。 完成此 OID 请求后，源主机上的网络适配器连接将通过 oid [ \_ 交换机 \_ NIC \_ 删除](./oid-switch-nic-delete.md)的 oid 设置请求删除。

    2.  删除网络适配器连接后，将通过 oid [ \_ 交换机 \_ 端口 \_ 拆卸](./oid-switch-port-teardown.md)的 oid 集请求来分解操作端口。 完成此 OID 请求后，将通过 oid \_ 交换机端口删除的 oid 设置请求删除操作端口 \_ \_ 。

5.  通过 oid [ \_ 交换机 \_ NIC \_ CREATE](./oid-switch-nic-create.md)的 oid 集请求，为目标主机上的操作端口创建网络适配器连接。 如果此 OID 请求成功完成，则通过 oid [ \_ 交换机 \_ NIC \_ CONNECT](./oid-switch-nic-connect.md)的 oid 集请求在关联的操作端口上建立网络适配器连接。

    如果成功建立网络适配器连接，则会在目标主机上还原操作端口和网络适配器连接的运行时数据。

    此时，基础扩展可以在网络适配器连接上执行资源保留和验证。

 

