---
title: OID_GEN_CO_LINK_SPEED
description: 本主题介绍 OID_GEN_CO_LINK_SPEED 对象标识符（OID）。
ms.assetid: a88ef1b9-b3f0-403e-8188-85aead46663f
keywords:
- OID_GEN_CO_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: edad21b56d642a77d337cbc6d6282a7a46c67c3e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917959"
---
# <a name="oid_gen_co_link_speed"></a>OID_GEN_CO_LINK_SPEED

OID_GEN_CO_LINK_SPEED OID 请求微型端口驱动程序返回其当前传输和接收速度，格式为 NDIS_CO_LINK_SPEED 结构，如下所示：

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

此结构的成员包含以下信息：

**出站**  
NIC 的当前传输速度。 度量单位为100bps，因此值100000表示硬件比特率为 10 Mbps。

**入站**  
NIC 的当前接收速度。 度量单位为100bps，因此值100000表示硬件比特率为 10 Mbps。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

