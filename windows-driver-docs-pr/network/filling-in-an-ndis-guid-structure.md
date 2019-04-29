---
title: 填充 NDIS_GUID 结构
description: 填充 NDIS_GUID 结构
ms.assetid: 971f6f25-fd2b-4a1e-9378-6270a094f4ff
keywords:
- NDIS_GUID
- WMI WDK 网络、 Guid
- Oid WDK 网络 WMI
- Guid WDK 网络
- Windows Management Instrumentation WDK 网络 Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdfb61c2baae1535debcc5e7095b914fa6157c56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380153"
---
# <a name="filling-in-an-ndisguid-structure"></a>填写 NDIS\_GUID 结构





NDIS\_GUID 结构定义，如下所示：

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

若要获取的 GUID **Guid**结构中的成员，您可以运行 Uuidgen.exe 应用程序。 有关此应用程序的详细信息，请参阅 Microsoft Windows SDK 文档。

**Oid**或**状态**成员是 ULONG 是 OID 代码。 NDIS 6.0 不映射到 WMI Guid 的自定义状态指示。

如果 NDIS\_GUID 结构映射返回数组的数据项，OID**大小**成员指定的大小，单位为字节数组中每个数据项。 如果数据不是一个数组**大小**成员指定数据的大小。 如果数据项的大小是变量，或如果 OID 不返回数据，**大小**成员必须为-1。

以下值的按位 OR**标志**成员指示的 GUID 与相关联的数据类型：

<a href="" id="fndis-guid-to-oid"></a>fNDIS\_GUID\_TO\_OID  
当设置此标志，NDIS\_GUID 结构映射到 OID 的 GUID。

<a href="" id="fndis-guid-to-status"></a>fNDIS\_GUID\_TO\_状态  
NDIS 为保留。 微型端口驱动程序不应使用此标志。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS\_GUID\_ANSI\_STRING  
当设置此标志时，以 null 结尾的 ANSI 字符串提供的 guid。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS\_GUID\_UNICODE\_字符串  
当设置此标志时，Unicode 字符串提供的 guid。

<a href="" id="fndis-guid-array"></a>fNDIS\_GUID\_ARRAY  
设置此标志，guid 提供数据的项的数组。 指定**大小**值指示数组中每个数据项的长度。

<a href="" id="fndis-guid-allow-read"></a>fNDIS\_GUID\_ALLOW\_READ  
当设置此标志时，允许所有用户使用此 GUID 来获取信息。

<a href="" id="fndis-guid-allow-write"></a>fNDIS\_GUID\_允许\_编写  
设置此标志，允许所有用户使用此 GUID 可以设置信息。

**请注意**  微型端口驱动程序提供的自定义 WMI Guid 是默认情况下，只有具有管理员权限的用户才能访问。 具有管理员权限的用户始终可以读取或写入一个自定义 GUID，如果微型端口驱动程序支持读取或写入该 GUID 的操作。 您可以设置 fNDIS\_GUID\_允许\_读取和 fNDIS\_GUID\_允许\_写标志以允许所有用户访问自定义 GUID。

 

请注意，对于一个驱动程序注册的所有自定义 Guid，该驱动程序必须设置 fNDIS\_GUID\_TO\_OID。 微型端口驱动程序应永远不会设置 fNDIS\_GUID\_TO\_状态。 所有其他标志可以组合使用位或运算。

 

 





