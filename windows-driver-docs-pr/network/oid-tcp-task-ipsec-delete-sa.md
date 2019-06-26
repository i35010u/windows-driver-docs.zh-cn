---
title: OID_TCP_TASK_IPSEC_DELETE_SA
description: 本主题介绍 OID_TCP_TASK_IPSEC_DELETE_SA 对象标识符 (OID)。
ms.assetid: 5f3b1f30-ab44-4d1c-96ff-b70ae6cfe324
keywords:
- OID_TCP_TASK_IPSEC_DELETE_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36503de3e132073f01fb0fab324c5e6bab12bd36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353720"
---
# <a name="oidtcptaskipsecdeletesa"></a>OID_TCP_TASK_IPSEC_DELETE_SA

传输协议设置 OID_TCP_TASK_IPSEC_DELETE_SA OID 以请求微型端口驱动程序从 NIC 中删除安全关联 (SA) SA 信息的格式为[OFFLOAD_IPSEC_DELETE_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_offload_ipsec_delete_sa)结构。

在接收到此请求，微型端口驱动程序应删除任何系统资源分配给 SA 指定的 SA 从 NIC 和免费。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

