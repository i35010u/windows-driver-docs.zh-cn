---
title: OID_CO_ADD_ADDRESS
description: 本主题介绍 OID_CO_ADD_ADDRESS 对象标识符 (OID)。
ms.assetid: ca6bb3eb-87db-4e71-9585-34cd1e978b6a
keywords:
- OID_CO_ADD_ADDRESS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2969e6314ebd2fb24b0ce09104070069811476cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363315"
---
# <a name="oidcoaddaddress"></a>OID_CO_ADD_ADDRESS

OID_CO_ADD_ADDRESS OID 是客户端发送到呼叫管理器为主机指定的别名地址。 别名地址格式为 CO_ADDRESS 定义的结构，按如下所示：

```c++
typedef struct _CO_ADDRESS{
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

此结构的成员包含下列信息：

**AddressSize**  
以字节为单位的结构在指定的大小**地址**。

**地址**  
指定长度可变的数组，其中包含的别名地址。 地址格式是特定于呼叫管理器使用的信号协议。

通常使用此 OID 来指定主机提供了特定服务的已知地址。 例如，客户端可以指定 LAN 仿真服务器的已知地址。 向此 OID 的呼叫管理器的响应是特定于呼叫管理器使用的信号协议。 ATM 调用管理器中，例如，将一条消息发送到通知的别名地址的开关的交换机。


## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

