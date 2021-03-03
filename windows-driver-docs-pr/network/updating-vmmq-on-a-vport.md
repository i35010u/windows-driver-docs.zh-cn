---
title: 启用、禁用和更新 VPort 上的 VMMQ
description: 创建 VPort 后，上层驱动程序可以启用、禁用或更新 VPort 的 RSS 参数。
ms.date: 02/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: a8892343772a207ecd8ab1ed79a17ff11da9fddf
ms.sourcegitcommit: cf1f4196374c5b743448cb8d688d2223f7197d8f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751966"
---
# <a name="enabling-disabling-and-updating-vmmq-on-a-vport"></a>启用、禁用和更新 VPort 上的 VMMQ

创建 VPort 后，上层驱动程序可以启用、禁用或更新 VPort 的 RSS 参数。 

驱动程序可更新 VPort 的 RSS 间接寻址表，以 [更改 VPort 的队列数](#changing-the-number-of-queues-for-a-vport)。 但是，VPort 的 RSS 哈希类型、哈希函数和哈希密钥将被视为静态参数，而在 VPort 的生存期内，过量驱动程序也不会对其进行更改。 如果上层驱动程序希望更改任何 RSS 静态参数，则必须删除并重新创建 VPort。

上层驱动程序通过发出 [oid 生成 \_ \_ 接收 \_ 刻度 \_ 参数](oid-gen-receive-scale-parameters.md) oid 请求，启用、禁用或更改 VPort 的 RSS 参数。 上层驱动程序将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中的 **VPortId** 字段设置为新配置的目标 VPort 的 ID。 

上层驱动程序还会设置 OID 请求中使用的 [**NDIS \_ 接收 \_ 缩放 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) 结构，如下所示。 请注意，根据基础微型端口适配器播发的 VMMQ 功能，某些字段可能会设置为所有 PF VPorts 的相同值。


- 将 **标头** 的 **修订** 成员设置为 **NDIS \_ 接收 \_ 缩放 \_ 参数 \_ 修订版本 \_ 3**。

- 设置 "NDIS \_ RSS \_ 参数 \_ 标志 \_ 默认 \_ 处理器 \_ 未更改" 标志，以指定 **DefaultProcessorNumber** 成员未发生更改。

- 将 **BaseCpuNumber** 设置为 **零**。

- 设置 **DefaultProcessorNumber** 以指定此 VPort 的默认 RSS 处理器。 小型端口可以假设默认处理器是 RSS 处理器列表的一部分，但它不能假定默认的 RSS 处理器在当前的间接寻址表中。 

- 设置 **HashInformation** 以指示 NIC 应该用于计算此 VPort 接收的数据包的哈希值的哈希类型和哈希函数。 上层驱动程序可以将此字段设置为每个 VPort 的不同值。

- 设置 **IndirectionTableSize** 以指定间接寻址表的大小（以字节为单位）。 将此字段设置为所有 PF VPorts 的相同值。 上层驱动程序必须确保间接表中的条目数为2的幂。

- 设置 **IndirectionTableOffset** ，以指定从 [**NDIS \_ 接收 \_ 刻度 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) 结构开始的间接寻址表的偏移量。

- 设置 **HashSecretKeySize** 以指定哈希机密密钥的大小（以字节为单位）。 如果微型端口适配器支持此，则上层驱动程序可能为每个 VPort 设置不同的密钥。 有关详细信息，请参阅 [播发 VMMQ 功能](advertising-vmmq-capabilities.md)。

- 设置 **HashSecretKeyOffset** ，以指定从 [**NDIS \_ 接收 \_ 刻度 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) 结构开始的哈希机密密钥的偏移量。 如果微型端口适配器支持此，则上层驱动程序可能为每个 VPort 设置不同的密钥。 有关详细信息，请参阅 [播发 VMMQ 功能](advertising-vmmq-capabilities.md)。

- 适当地设置 **ProcessorMaskOffset**、 **NumberOfProcessorMasks** 和 **ProcessorMasksEntrySize** 。

当微型端口驱动程序接收到对 VPort 禁用 VMMQ 的 OID 请求时，它应还原为在由在 [oid \_ nic \_ switch \_ CREATE \_ VPort](oid-nic-switch-create-vport.md) oid 请求中使用的 [NDIS \_ nic \_ 交换机 \_ VPort \_ 参数](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构中的 **ProcessorAffinity** 字段指定的处理器上收到的所有数据包。

## <a name="changing-the-number-of-queues-for-a-vport"></a>更改 VPort 的队列数

在 VPort 的间接寻址表中使用的唯一处理器数不能超过上一次颁发的 [oid \_ nic \_ 交换机 \_ CREATE \_ VPort](oid-nic-switch-create-vport.md) OID 请求中指定的 [**NDIS \_ nic \_ 交换机 \_ VPort \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的 **NumQueuePairs** 字段的值。 这些处理器将是通过调用 [**NdisGetRssProcessorInformation**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation)返回的 RSS 处理器集的子集。 有关详细信息，请参阅 [分配 VPorts FOR VMMQ](allocating-vports-for-vmmq.md)。 但是，不同 VPorts 上的间接寻址表可能包含相同的处理器。

若要减少 PF VPort 上层驱动程序的队列数量，必须执行以下操作：

1. 使用原始的间接寻址表大小发送 [oid 生成 \_ \_ 接收 \_ 刻度 \_ 参数](oid-gen-receive-scale-parameters.md) oid。 但是，此步骤中的间接寻址表只能引用最多新队列数的非重复处理器数。 如果由于 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构的 NDIS_NIC_SWITCH_CAPS_RSS_PER_PF_VPORT_INDIRECTION_TABLE_SIZE_RESTRICTED 标志，新的间接寻址表需要小于原始表，则颁发者必须确保此步骤中的间接寻址表将包含新的间接寻址表，并根据需要多次复制，以满足原始队列数的限制标志要求。

2. 发送具有新队列数的 [OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md) OID。

3. 如果已更改，则使用新的间接表大小发送 OID_GEN_RECEIVE_SCALE_PARAMETERS。

若要增加 PF VPort 上层驱动程序的队列数量，必须执行以下操作：

1. 该驱动程序不需要在步骤2之前更新当前的间接寻址表，因为该表只引用最多为当前队列数的不同处理器数。

2. 发送具有新队列数的 [OID_NIC_SWITCH_VPORT_PARAMETERS](oid-nic-switch-vport-parameters.md) OID。 如果设置了限制标志，微型端口驱动程序应根据需要在内部复制原始间接寻址表，以匹配新队列数的间接寻址表大小要求。

3. 如果已更改，则使用新的间接表大小发送 [oid 生成 \_ \_ 接收 \_ 刻度 \_ 参数](oid-gen-receive-scale-parameters.md) oid。


