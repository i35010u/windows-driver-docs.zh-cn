---
title: OID_GEN_CO_MINIMUM_LINK_SPEED
description: 本主题介绍) OID_GEN_CO_MINIMUM_LINK_SPEED 对象标识符 (OID。
keywords:
- OID_GEN_CO_MINIMUM_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a20ca3192710129d46074cc2eb06b9b6cdd91a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836769"
---
# <a name="oid_gen_co_minimum_link_speed"></a>OID_GEN_CO_MINIMUM_LINK_SPEED

OID_GEN_CO_MINIMUM_LINK_SPEED OID 请求微型端口驱动程序返回其最小传输和接收速度，格式为 NDIS_CO_LINK_SPEED 结构，如下所示：

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

此结构的成员包含以下信息：

**Outbound**  
NIC 的最小传输速率。 度量单位为100bps，因此值100000表示硬件比特率为 10 Mbps。

**入站**  
NIC 的最小接收速度。 度量单位为100bps，因此值100000表示硬件比特率为 10 Mbps。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

