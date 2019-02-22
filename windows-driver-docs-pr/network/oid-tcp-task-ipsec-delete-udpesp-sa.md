---
title: OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
description: 本主题介绍 OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA 对象标识符 (OID)。
ms.assetid: f598199e-48f2-4ff5-846e-e88139408824
keywords:
- OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6db1e451d9bb86309e766caf6cc7e7585d890ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545834"
---
# <a name="oidtcptaskipsecdeleteudpespsa"></a>OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA

传输协议设置 OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA 以请求微型端口驱动程序从 NIC 分析器条目列表删除 UDP ESP 安全关联 (SA) 和分析器条目 （可能）。 SA 和分析器项信息的格式为[OFFLOAD_IPSEC_DELETE_UDPESP_SA](https://msdn.microsoft.com/library/windows/hardware/ff569059)结构。

如果**EncapTypeEntryOffldHandle**是**NULL**、 微型端口应从 NIC 中删除指定的 SA 和 sa 分配任何系统资源的免费。 如果**EncapTypeEntryOffldHandle**为非**NULL**，微型端口还应从 NIC 的分析器条目列表中删除指定的分析器条目。

请注意，传输协议就可以请求微型端口，以便完成微型端口添加该 SA 和/或分析器条目之前删除 SA 和/或分析程序条目。 因此，微型端口必须序列化具有加法运算的删除操作。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

