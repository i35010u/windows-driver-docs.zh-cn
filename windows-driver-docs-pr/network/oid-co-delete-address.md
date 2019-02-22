---
title: OID_CO_DELETE_ADDRESS
description: 本主题介绍 OID_CO_DELETE_ADDRESS 对象标识符 (OID)。
ms.assetid: 987c839b-f673-4c7a-90b4-fc5f93454b2e
keywords:
- OID_CO_DELETE_ADDRESS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 271061deee0f234432fe0de82fbc52a42c665736
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542903"
---
# <a name="oidcodeleteaddress"></a>OID_CO_DELETE_ADDRESS

OID_CO_DELETE_ADDRESS OID 是客户端发送到呼叫管理器主机中删除的别名地址。 别名地址格式为 CO_ADDRESS 定义的结构，按如下所示：

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS; 
```

此结构的成员包含下列信息：

**AddressSize**  
指定的大小以字节为单位的地址的结构。

**地址**  
指定长度可变的数组，其中包含的别名地址。 地址格式是特定于呼叫管理器使用的信号协议。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

