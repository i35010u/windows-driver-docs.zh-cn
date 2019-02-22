---
title: OID_GEN_CO_MINIMUM_LINK_SPEED
description: 本主题介绍 OID_GEN_CO_MINIMUM_LINK_SPEED 对象标识符 (OID)。
ms.assetid: 2ed27ec7-b773-4751-96d3-42d839f35a97
keywords:
- OID_GEN_CO_MINIMUM_LINK_SPEED
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8df5f23d62dd9be3be1a8768581aa0aefdd8ac5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555411"
---
# <a name="oidgencominimumlinkspeed"></a>OID_GEN_CO_MINIMUM_LINK_SPEED

OID_GEN_CO_MINIMUM_LINK_SPEED OID 请求微型端口驱动程序，若要返回其最小传输和接收速度格式，如下所示定义一个 NDIS_CO_LINK_SPEED 结构为：

```c++
typedef struct _NDIS_CO_LINK_SPEED{
    ULONG   Outbound;
    ULONG   Inbound;
} NDIS_CO_LINK_SPEED, *PNDIS_CO_LINK_SPEED;
```

此结构的成员包含下列信息：

**出站**  
最小传输速度的 nic。 度量单位是 100 bps，因此值为 100,000 表示的硬件比特率为 10 Mbps。

**入站**  
最小的接收速度的 nic。 度量单位是 100 bps，因此值为 100,000 表示的硬件比特率为 10 Mbps。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

