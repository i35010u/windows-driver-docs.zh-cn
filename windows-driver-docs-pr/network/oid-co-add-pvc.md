---
title: OID_CO_ADD_PVC
description: 本主题介绍 OID_CO_ADD_PVC 对象标识符（OID）。
ms.assetid: 182d5bdb-9cfe-4e9c-a2cf-4d5440bfdb76
keywords:
- OID_CO_ADD_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24cf68553e157aeff5eb840d9d15e083f243b63f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843270"
---
# <a name="oid_co_add_pvc"></a>OID_CO_ADD_PVC

OID_CO_ADD_PVC OID 由客户端发送到呼叫管理器，以将永久虚拟连接（PVC）添加到呼叫管理器的已配置 Pvc 列表。 PVC 的格式为 CO_PVC 结构，定义如下：

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
```

此结构的成员包含以下信息：

**NdisAfHandle**  
指定由[NdisClOpenAddressFamilyEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)返回的 NDIS 提供的句柄。

**PvcParameters**  
格式[CO_SPECIFIC_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))结构。 此结构包含用于描述 PVC 的特定于协议的参数。

PVC 由管理员手动配置。 监视此类活动的客户端通过将此 OID 发送到呼叫管理器通知新配置的 PVC 的呼叫管理器。 然后，其他客户端可以使用新配置的 PVC。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis （包括 Ndis .h） |

