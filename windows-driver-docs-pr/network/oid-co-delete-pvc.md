---
title: OID_CO_DELETE_PVC
description: 本主题介绍) OID_CO_DELETE_PVC 对象标识符 (OID。
ms.assetid: 02da08d0-9d08-4a91-b851-50e3c3b065d6
keywords:
- OID_CO_DELETE_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e634bc2b442ef57c9946a74dd581ccc723020d3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214648"
---
# <a name="oid_co_delete_pvc"></a>OID_CO_DELETE_PVC

OID_CO_DELETE_PVC OID 由客户端发送到呼叫管理器，以从已配置的 Pvc 的 "呼叫管理器" 列表中删除 (PVC) 的永久虚拟连接。 PVC 的格式为 CO_PVC 结构，定义如下：

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
``` 

此结构的成员包含以下信息：

**NdisAfHandle**  
指定由 [NdisClOpenAddressFamilyEx](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)返回的 NDIS 提供的句柄。

**PvcParameters**  
格式 [CO_SPECIFIC_PARAMETERS](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex) 的结构。 此结构包含用于描述 PVC 的特定于协议的参数。

管理员手动删除 PVC。 监视此类活动的客户端会向调用管理器发送此 OID，通知已删除的 PVC 的调用管理器。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 