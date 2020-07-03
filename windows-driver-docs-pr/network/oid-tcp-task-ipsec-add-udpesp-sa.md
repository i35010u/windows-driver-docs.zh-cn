---
title: OID_TCP_TASK_IPSEC_ADD_UDPESP_SA
description: 本主题介绍 OID_TCP_TASK_IPSEC_ADD_UDPESP_SA 对象标识符（OID）。
ms.assetid: 022db6dd-1099-4069-81af-7f919d91464e
keywords:
- OID_TCP_TASK_IPSEC_ADD_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 479d5fc6a1d748aba2e27adf0703ad6878935bc9
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917623"
---
# <a name="oid_tcp_task_ipsec_add_udpesp_sa"></a>OID_TCP_TASK_IPSEC_ADD_UDPESP_SA

传输协议将 OID_TCP_TASK_IPSEC_ADD_UDPESP_SA 设置为请求微型端口驱动程序，以便将 UDP 封装的 ESP 数据包的一个或多个安全关联（SAs）添加到 NIC。

每个 SA 的信息被格式化为[OFFLOAD_IPSEC_ADD_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_add_udpesp_sa)结构。 请注意，此结构与[OID_TCP_TASK_IPSEC_ADD_SA](oid-tcp-task-ipsec-add-sa.md)请求中使用的[OFFLOAD_IPSEC_ADD_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_add_sa)结构几乎完全相同。 唯一的区别是 OFFLOAD_IPSEC_ADD_UDPESP_SA 结构包含**EncapTypeEntry**和**EncapTypeEntryOffldHandle**成员。

OFFLOAD_IPSEC_ADD_UDPESP_SA 结构的前七个成员（**SrcAddr**、 **SrcMask**、 **DestAddr**、 **DestMask**、 **Protocol**、 **SrcPort**和**DestPort**）组成了一个筛选器，该筛选器指定 SAs 适用的源和目标以及 IP 协议。 此筛选器适用于传输模式连接，即两个主机之间的端到端连接。 如果通过隧道建立指定的连接，则隧道的源地址和目标地址将分别由**SrcTunnelAddr**和**DestTunnelAddr**指定。

如果筛选器参数设置为零，则不会使用该参数来筛选指定 SAs 的数据包。 例如，如果**SrcAddr**设置为零，则指定的 SAs 可以应用于包含任何源地址的数据包。 为此，如果所有筛选器参数均设置为零，则指定的 SAs 适用于向任何目标主机发送任意类型的数据包的任何源主机。

TCP/IP 传输可在**协议**成员中指定 IP 协议，以指示指定的 SAs 仅适用于指定协议类型的数据包。 如果 "**协议**" 设置为零，则指定的 SAs 适用于从指定的源发送到指定目标的所有数据包。

## <a name="offload_security_association-structure"></a>OFFLOAD_SECURITY_ASSOCIATION 结构

[OFFLOAD_SECURITY_ASSOCIATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_security_association)结构指定单个安全关联（SA）。 OFFLOAD_SECURITY_ASSOCIATION 结构是**SecAssoc**变长数组中的一个元素。 **SecAssoc**包含一个或两个 OFFLOAD_SECURITY_ASSOCIATION 结构。

指定用于处理身份验证标头（AH）的 SA 的操作类型为 "**身份验证**"，并且将具有**IntegrityAlgo** （完整性算法）。 SA 不会有**ConfAlgo** （机密性算法）。 在这种情况下， **ConfAlgo**将包含零。

指定用于处理封装式安全负载（ESPs）的 SA 的操作类型为 "**加密**"，可能具有**IntegrityAlgo** （完整性算法）和/或**ConfAlgo** （机密性算法）。

## <a name="offload_algo_info-structure"></a>OFFLOAD_ALGO_INFO 结构

[OFFLOAD_ALGO_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_algo_info)结构是[OFFLOAD_SECURITY_ASSOCIATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_security_association)结构的成员，它指定用于安全关联（SA）的算法。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

