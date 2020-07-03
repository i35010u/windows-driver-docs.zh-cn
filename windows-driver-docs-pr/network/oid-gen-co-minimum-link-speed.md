---
title: OID_GEN_CO_MINIMUM_LINK_SPEED
description: 本主题介绍 OID_GEN_CO_MINIMUM_LINK_SPEED 对象标识符（OID）。
ms.assetid: 2ed27ec7-b773-4751-96d3-42d839f35a97
keywords:
- OID_GEN_CO_MINIMUM_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4cfe31f6c01081656c99c31144bbeef481d04c0
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917499"
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

**出站**  
NIC 的最小传输速率。 度量单位为100bps，因此值100000表示硬件比特率为 10 Mbps。

**入站**  
NIC 的最小接收速度。 度量单位为100bps，因此值100000表示硬件比特率为 10 Mbps。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

