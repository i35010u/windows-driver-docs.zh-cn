---
title: 填充 NDIS_GUID 结构
description: 填充 NDIS_GUID 结构
keywords:
- NDIS_GUID
- WMI WDK 网络，Guid
- Oid WDK 网络，WMI
- Guid WDK 网络
- Windows Management Instrumentation WDK 网络，Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d396bccb22c5aa813ee9ae3652e956fb12132400
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795987"
---
# <a name="filling-in-an-ndis_guid-structure"></a>填充 NDIS \_ GUID 结构





NDIS \_ GUID 结构定义如下：

```C++
typedef struct _NDIS_GUID {
  GUID  Guid;
  union {
    NDIS_OID  Oid;
    NDIS_STATUS  Status;
  };
  ULONG  Size;
  ULONG  Flags;
} NDIS_GUID, *PNDIS_GUID;
```

若要获取结构的 **guid** 成员的 guid，可以运行 Uuidgen.exe 应用程序。 有关此应用程序的详细信息，请参阅 Microsoft Windows SDK 文档。

**Oid** 或 **Status** 成员是作为 Oid 代码的 ULONG。 NDIS 6.0 不会将自定义状态指示映射到 WMI Guid。

如果 NDIS \_ GUID 结构映射了返回数据项数组的 OID，则 **Size** 成员指定数组中每个数据项的大小（以字节为单位）。 如果数据不是数组，则 **size** 成员指定数据的大小。 如果数据项的大小是可变的，或者如果 OID 不返回数据，则 **size** 成员必须为-1。

**Flags** 成员的下列值的按位 "或" 指示与 GUID 关联的数据类型：

<a href="" id="fndis-guid-to-oid"></a>fNDIS \_ GUID \_ 到 \_ OID  
设置此标志后，NDIS \_ guid 结构将 guid 映射到 OID。

<a href="" id="fndis-guid-to-status"></a>fNDIS \_ GUID \_ 到 \_ 状态  
为 NDIS 预留。 微型端口驱动程序不应使用此标志。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS \_ GUID \_ ANSI \_ 字符串  
设置此标志后，将为 GUID 提供以 null 结尾的 ANSI 字符串。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS \_ GUID \_ UNICODE \_ 字符串  
设置此标志后，将为 GUID 提供一个 Unicode 字符串。

<a href="" id="fndis-guid-array"></a>fNDIS \_ GUID \_ 数组  
设置此标志后，将为 GUID 提供数据项的数组。 指定的 **大小** 值指示数组中每个数据项的长度。

<a href="" id="fndis-guid-allow-read"></a>fNDIS \_ GUID \_ 允许 \_ 读取  
设置此标志后，所有用户都可以使用此 GUID 获取信息。

<a href="" id="fndis-guid-allow-write"></a>fNDIS \_ GUID \_ 允许 \_ 写入  
设置此标志后，允许所有用户使用此 GUID 设置信息。

**注意**  默认情况下，只有具有管理员权限的用户才能访问微型端口驱动程序提供的自定义 WMI Guid。 如果微型端口驱动程序支持该 GUID 的读取或写入操作，则具有管理员权限的用户始终可以读取或写入自定义 GUID。 可以设置 fNDIS \_ guid \_ allow \_ READ 和 fNDIS \_ guid \_ allow \_ 写入标志，以允许所有用户访问自定义 GUID。

 

请注意，对于驱动程序注册的所有自定义 Guid，驱动程序必须将 fNDIS \_ GUID 设置 \_ 为 \_ OID。 微型端口驱动程序绝不应将 fNDIS \_ GUID 设置 \_ 为 \_ STATUS。 所有其他标志都可以使用按位 "或" 运算组合在一起。

 

 





