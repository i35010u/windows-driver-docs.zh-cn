---
title: OID_CO_GET_ADDRESSES
description: 本主题介绍) OID_CO_GET_ADDRESSES 对象标识符 (OID。
keywords:
- OID_CO_GET_ADDRESSES
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 172ea6e421b5c743bc3e56b0f38cff57e0f299a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806185"
---
# <a name="oid_co_get_addresses"></a>OID_CO_GET_ADDRESSES

OID_CO_GET_ADDRESSES OID 由客户端用于向调用管理器发出查询。 此查询用于响应将 OID_CO_ADDRESS_CHANGE 发送到客户端的调用管理器。 对于此查询，调用管理器会向客户端发送一个格式为 CO_ADDRESS_LIST 结构的地址列表，定义如下：

```c++
typedef struct _CO_ADDRESS_LIST {
    ULONG       NumberOfAddressesAvailable;
    ULONG       NumberOfAddresses;
    CO_ADDRESS  AddressList;
} CO_ADDRESS_LIST, *PCO_ADDRESS_LIST;
```

此结构的成员包含以下信息：

**NumberOfAddressesAvailable**  
指定呼叫管理器的地址列表中的最大地址数。 无论调用管理器在 **AddressList** 返回到客户端的地址的实际数量如何， **AddressList** 的缓冲区大小始终为 **NumberOfAddressesAvailable** 乘以地址大小，该大小是特定于调用管理器的固定大小。

**NumberOfAddresses**  
指定调用管理器写入 **AddressList** 的地址的数目。

**AddressList**  
别名地址的格式为 CO_ADDRESS 结构，定义如下：

```c++
typedef struct _CO_ADDRESS {
    ULONG   AddressSize;
    UCHAR   Address[1];
} CO_ADDRESS, *PCO_ADDRESS;
```

此结构的成员包含以下信息：

**AddressSize**  
指定 **地址** 处的结构的大小（以字节为单位）。

**Address**  
指定包含地址列表的可变长度数组。 地址格式特定于呼叫管理器使用的信号协议。

**AddressList** 包含可用于访问本地主机的网络地址。 返回到特定客户端的 **AddressList** 包含所有客户端共用的地址，以及该客户端自行添加到 OID_CO_ADD_ADDRESS 的地址列表中的所有地址。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

