---
title: OID_TCP_TASK_IPSEC_DELETE_SA
description: 本主题介绍) OID_TCP_TASK_IPSEC_DELETE_SA 对象标识符 (OID。
keywords:
- OID_TCP_TASK_IPSEC_DELETE_SA
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a97d2f57a41495367731942333a088262775d83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823841"
---
# <a name="oid_tcp_task_ipsec_delete_sa"></a>OID_TCP_TASK_IPSEC_DELETE_SA

OID_TCP_TASK_IPSEC_DELETE_SA OID 由传输协议设置，以请求微型端口驱动程序从 NIC (SA) 删除安全关联。 SA 信息的格式设置为 [OFFLOAD_IPSEC_DELETE_SA](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_offload_ipsec_delete_sa) 结构。

收到此请求后，微型端口驱动程序应从 NIC 中删除指定的 SA，并释放为 SA 分配的任何系统资源。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
