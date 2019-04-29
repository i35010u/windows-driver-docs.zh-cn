---
title: OID_GEN_CO_LINK_SPEED
description: 本主题介绍 OID_GEN_CO_LINK_SPEED 对象标识符 (OID)。
ms.assetid: a88ef1b9-b3f0-403e-8188-85aead46663f
keywords:
- OID_GEN_CO_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 604d057c478e3ffa66488e0d89abe760633cf019
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379221"
---
# <a name="oidgencolinkspeed"></a>OID_GEN_CO_LINK_SPEED

OID_GEN_CO_LINK_SPEED OID 请求微型端口驱动程序，若要返回其当前传输和接收速度格式，如下所示定义一个 NDIS_CO_LINK_SPEED 结构为：

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

此结构的成员包含下列信息：

**出站**  
当前的传输速度的 nic。 度量单位是 100 bps，因此值为 100,000 表示的硬件比特率为 10 Mbps。

**入站**  
当前的接收速度的 nic。 度量单位是 100 bps，因此值为 100,000 表示的硬件比特率为 10 Mbps。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

