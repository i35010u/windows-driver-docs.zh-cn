---
title: OID_CO_GET_ADDRESSES
description: 本主题介绍 OID_CO_GET_ADDRESSES 对象标识符 (OID)。
ms.assetid: 0c30e184-be01-49ab-b9ad-3ccc2fdf9fc5
keywords:
- OID_CO_GET_ADDRESSES
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9004aadc69b1a2d2afa3d9b1ab426cc77df8adb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523500"
---
# <a name="oidcogetaddresses"></a>OID_CO_GET_ADDRESSES

客户端使用 OID_CO_GET_ADDRESSES OID 对呼叫管理器进行查询。 此查询将响应发送到客户端 OID_CO_ADDRESS_CHANGE 呼叫管理器中。 此查询的响应，呼叫管理器客户端设置的格式的地址列表将作为发送 CO_ADDRESS_LIST 定义的结构，按如下所示：

```c++
typedef struct _CO_ADDRESS_LIST {
    ULONG       NumberOfAddressesAvailable;
    ULONG       NumberOfAddresses;
    CO_ADDRESS  AddressList;
} CO_ADDRESS_LIST, *PCO_ADDRESS_LIST;
```

此结构的成员包含下列信息：

**NumberOfAddressesAvailable**  
在调用管理器的地址列表中指定的最大地址数。 而不考虑呼叫管理器返回到客户端在地址的实际数目**AddressList**，在缓冲区的大小**AddressList**始终**NumberOfAddressesAvailable**地址大小，这是特定于呼叫管理器的固定的大小的乘积。

**NumberOfAddresses**  
指定的呼叫管理器已写入到的地址数**AddressList**。

**AddressList**  
别名地址格式为 CO_ADDRESS 定义的结构，按如下所示：

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

此结构的成员包含下列信息：

**AddressSize**  
以字节为单位的结构在指定的大小**地址**。

**地址**  
指定长度可变的数组，其中包含的地址列表。 地址格式是特定于呼叫管理器使用的信号协议。

**AddressList**包含用于访问本地主机的网络地址。 **AddressList**返回到特定客户端包含共有的所有客户端的地址，以及客户端本身已添加到呼叫管理器的列表具有 OID_CO_ADD_ADDRESS 地址的任何地址。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

