---
title: HYPER-V 可扩展交换机实时迁移支持
description: HYPER-V 可扩展交换机实时迁移支持
ms.assetid: 4AFC9E3F-C9C5-4693-BA8C-BC7122A4055F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 027b8b09f76383277e3f69ac8eef00c0529fbcce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522136"
---
# <a name="hyper-v-extensible-switch-live-migration-support"></a>HYPER-V 可扩展交换机实时迁移支持


在 HYPER-V 实时迁移，子分区，或*虚拟机 (VM)*，在一台主机计算机上停止 (*源主机*) 和迁移到另一台主机计算机 (*目标主机*). 在实时迁移期间将发生以下操作：

-   当源主机上启动实时迁移时，可扩展交换机接口请求基础的扩展，以保存每个端口和其关联的网络适配器连接的运行时数据。

    有关此操作的详细信息，请参阅[HYPER-V 可扩展交换机保存操作](hyper-v-extensible-switch-save-operations.md)。

-   目标主机上的实时迁移完成之前，可扩展交换机接口请求以还原每个端口和其关联的网络适配器连接的运行时数据的基础扩展。

    有关此操作的详细信息，请参阅[HYPER-V 可扩展交换机还原操作](hyper-v-extensible-switch-restore-operations.md)。

在实时迁移的设置阶段，源主机创建与目标物理主机的 TCP 连接。 HYPER-V 将通过此连接源 VM 的配置数据传输到目标物理主机。 主干 VM 上设置目标主机和内存分配给目标虚拟机。 现在，HYPER-V 将传输源 VM 的状态，包括其内存页，为目标虚拟机。

可扩展交换机接口也使用 TCP 连接来实时迁移期间同步步骤和结果。 例如，在目标主机运行的接口与已迁移的 VM 关联的端口和网络适配器连接的源主机从请求运行时数据的传输。

在 VM 进入联机状态目标主机的目标之前, 的可扩展交换机接口执行以下步骤：

1.  通过对象标识符 (OID) 组请求的目标主机上创建验证端口[OID\_交换机\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)。 如果已成功创建端口，可扩展交换机接口发出其他 OID 请求验证的基础扩展的端口策略的属性。

    如果该扩展的端口创建失败或使失效的任何策略属性中，实时迁移不会继续该目标节点和切换。

    有关验证端口和其用法的详细信息，请参阅[验证端口](validation-ports.md)。

2.  验证端口的策略属性验证是否已成功完成后，会删除通过 OID 集请求的目标主机上[OID\_交换机\_端口\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598273)。 删除此端口后，目标主机上创建一个操作的端口，并在其原位置创建操作的端口。 [ **NDIS\_交换机\_端口\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598229)与关联的结构[OID\_交换机\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)操作端口的请求包含相同的数据用于在源主机上创建该端口。

    如果成功创建操作的端口，端口策略添加到操作端口。

3.  如果在目标主机上，保存操作的端口已成功应用设置为源主机上的操作端口发出操作。

4.  如果保存操作成功完成，操作的端口和其网络适配器连接源主机上删除如下所示：

    1.  首先通过 OID 集请求的已断开连接的网络连接[OID\_交换机\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)。 源主机上的网络适配器连接此 OID 请求完成后，会删除通过 OID 集请求的[OID\_交换机\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)。

    2.  删除网络适配器连接后，操作的端口，则将调用通过 OID 集请求的[OID\_交换机\_端口\_拆卸](https://msdn.microsoft.com/library/windows/hardware/hh598279)。 完成此 OID 请求后，通过 OID 的 OID 集请求删除操作的端口\_交换机\_端口\_删除。

5.  为通过 OID 集请求的目标主机上运行的端口创建一个网络适配器连接[OID\_交换机\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)。 如果此 OID 请求成功完成，关联的操作通过 OID 集请求的端口上建立的网络适配器连接[OID\_交换机\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)。

    如果成功建立连接的网络适配器，则在目标主机上还原操作的端口和网络适配器连接的运行时数据。

    此时，基础扩展可以执行资源预留和验证的网络适配器连接上。

 

 





