---
title: OID_TCP_TASK_IPSEC_ADD_SA
description: 本主题介绍 OID_TCP_TASK_IPSEC_ADD_SA 对象标识符 (OID)。
ms.assetid: 7062c0df-627c-4110-a69f-ebad60f4e3b8
keywords:
- OID_TCP_TASK_IPSEC_ADD_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c9b2fdb64569c8fbc635338436b3fd6e7e821b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354135"
---
# <a name="oidtcptaskipsecaddsa"></a>OID_TCP_TASK_IPSEC_ADD_SA

传输协议设置 OID_TCP_TASK_IPSEC_ADD_SA OID 以请求微型端口驱动程序将一个或多个安全关联 (Sa) 添加到 nic。

每个 SA 的信息的格式为[OFFLOAD_IPSEC_ADD_SA](https://msdn.microsoft.com/library/windows/hardware/ff569056)结构。

OFFLOAD_IPSEC_ADD_SA 结构的前七个成员 (**模式筛选器**， **SrcMask**， **DestAddr**， **DestMask**， **协议**， **SrcPort**，并**DestPort**) 构成指定源和目标，以及 IP 协议，SAs 将应用的筛选器。 此筛选器与传输模式连接--即，两个主机之间的端到端连接。 如果通过隧道建立了指定的连接，指定源和目标地址的隧道**SrcTunnelAddr**并**DestTunnelAddr**分别。

如果筛选器参数设置为零，该参数不用于指定 SAs 来筛选数据包。 例如，如果**模式筛选器**设置为零，指定的 SAs 可以应用到包含任何源地址的数据包。 若要考虑到这极端的情况下，如果所有筛选器参数设置为零，指定的 SAs 适用于任何类型的数据包发送到任何目标主机的任何源主机。

TCP/IP 传输可以指定在 IP 协议**协议**成员来指示，指定的 SAs 仅适用于指定的协议类型的数据包。 如果**协议**设置为零，指定的 SAs 将应用到从指定的源发送到指定的目标的所有数据包。

## <a name="offloadsecurityassociation-structure"></a>OFFLOAD_SECURITY_ASSOCIATION 结构

[OFFLOAD_SECURITY_ASSOCIATION](https://msdn.microsoft.com/library/windows/hardware/ff569061)结构指定单独的安全关联 (SA)。 OFFLOAD_SECURITY_ASSOCIATION 结构是中的元素**SecAssoc**变长数组。 **SecAssoc**包含一个或两个 OFFLOAD_SECURITY_ASSOCIATION 结构。

在处理身份验证标头 (AH) 的使用将有的操作类型为指定的 SA**进行身份验证**并且将具有**IntegrityAlgo** （完整性算法）。 SA 不会**ConfAlgo** （保密性算法）。 在这种情况下， **ConfAlgo**将包含零。

在处理封装安全有效负载 (Esp) 的使用将有的操作类型为指定的 SA **ENCRYPT** ，并可能**IntegrityAlgo** （完整性算法） 和/或**ConfAlgo** （保密性算法）。

## <a name="offloadalgoinfo-structure"></a>OFFLOAD_ALGO_INFO 结构

[OFFLOAD_ALGO_INFO](https://msdn.microsoft.com/library/windows/hardware/ff568842)结构，它是成员的[OFFLOAD_SECURITY_ASSOCIATION](https://msdn.microsoft.com/library/windows/hardware/ff569061)结构，指定安全关联 (SA) 所使用的算法。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

