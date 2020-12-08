---
title: OID_CO_DELETE_PVC
description: 本主题介绍) OID_CO_DELETE_PVC 对象标识符 (OID。
keywords:
- OID_CO_DELETE_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70ac5f859e04c605097be87d9fae7043afc8cba9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806197"
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
