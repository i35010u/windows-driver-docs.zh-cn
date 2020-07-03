---
title: OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
description: 本主题介绍 OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA 对象标识符（OID）。
ms.assetid: f598199e-48f2-4ff5-846e-e88139408824
keywords:
- OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf20a103e053ddd7ea0d068b955f20c358b1d25
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916435"
---
# <a name="oid_tcp_task_ipsec_delete_udpesp_sa"></a>OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA

传输协议将 OID_TCP_TASK_IPSEC_DELETE_UDPESP_SA 设置为请求微型端口驱动程序从 NIC 分析器条目列表中删除 UDP ESP 安全关联（SA）和分析器条目（可能为分析器条目）。 SA 和分析器条目信息被格式化为[OFFLOAD_IPSEC_DELETE_UDPESP_SA](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_delete_udpesp_sa)结构。

如果**EncapTypeEntryOffldHandle**为**NULL**，则微型端口应从 NIC 中删除指定的 sa，并释放为 SA 分配的任何系统资源。 如果**EncapTypeEntryOffldHandle**不为**NULL**，则微型端口还应从 NIC 的分析器条目列表中删除指定的分析器条目。

请注意，在微型端口完成添加 SA 和/或分析器条目之前，传输协议可能会请求一个微型端口来删除 SA 和/或分析器条目。 因此，小型端口必须用加法运算序列化删除操作。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

