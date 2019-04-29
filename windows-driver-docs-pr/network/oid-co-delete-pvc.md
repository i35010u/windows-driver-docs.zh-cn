---
title: OID_CO_DELETE_PVC
description: 本主题介绍 OID_CO_DELETE_PVC 对象标识符 (OID)。
ms.assetid: 02da08d0-9d08-4a91-b851-50e3c3b065d6
keywords:
- OID_CO_DELETE_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd49afd8bca4bae0f4c37858374fa2e4e7f13120
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363281"
---
# <a name="oidcodeletepvc"></a>OID_CO_DELETE_PVC

OID_CO_DELETE_PVC OID 是由客户端向发送呼叫管理器删除永久性虚拟连接 (PVC) 从配置 Pvc 的呼叫管理器的列表。 PVC 格式化为 CO_PVC 定义的结构，按如下所示：

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
``` 

此结构的成员包含下列信息：

**NdisAfHandle**  
指定返回的 NDIS 提供句柄[NdisClOpenAddressFamilyEx](https://msdn.microsoft.com/library/windows/hardware/ff561639)。

**PvcParameters**  
一个格式化[CO_SPECIFIC_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff561639)结构。 此结构包含描述 PVC 的特定于协议的参数。

管理员手动删除 PVC。 监视此类活动的客户端通知已删除通过呼叫管理器向发送此 OID PVC 呼叫管理器。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

