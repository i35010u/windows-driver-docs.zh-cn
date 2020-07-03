---
title: OID_GEN_CO_SUPPORTED_GUIDS
description: 本主题介绍 OID_GEN_CO_SUPPORTED_GUIDS 对象标识符（OID）。
ms.assetid: d82d6ecb-f70b-4fc2-97eb-331aafe1fe57
keywords:
- OID_GEN_CO_SUPPORTED_GUIDS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a8e50bf218e57f0bb653244c93db1f204cf2645
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917031"
---
# <a name="oid_gen_co_supported_guids"></a>OID_GEN_CO_SUPPORTED_GUIDS

OID_GEN_CO_SUPPORTED_GUIDS OID 请求微型端口驱动程序返回 NDIS_GUID 类型的结构的数组。 数组中的每个结构指定自定义的 GUID （全局唯一标识符）到自定义 OID 的映射，或指定给微型端口驱动程序通过[NdisMCoIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)发送的 NDIS_STATUS 的映射。

NDIS_GUID 结构的定义如下所示：

```c++
typedef struct _NDIS_GUID {
    GUID    Guid;
    union {
        NDIS_OID    Oid;
        NDIS_STATUS Status;
    };
    ULONG   Size;
    ULONG   Flags;
} NDIS_GUID, *PNDIS_GUID;
```

此结构的成员包含以下信息：

**Guid**  
为微型端口驱动程序定义的自定义 GUID。

**Oid**  
**Guid**映射到的自定义 OID。

**Status**  
**Guid**映射到的 NDIS_STATUS。

**大小**  
设置 fNDIS_GUID_ARRAY 标志后，**大小**指定微型端口驱动程序返回的数组中每个数据项的大小（以字节为单位）。 如果已设置 fNDIS_GUID_ANSI_STRING 或 fNDIS_GUID_NDIS_STRING 标志，则**Size**设置为-1。 否则， **size**指定 GUID 表示的数据项的大小（以字节为单位）。

**标记**  
以下标志可以运算在一起，以指示 GUID 是映射到 OID 还是映射到 NDIS_STATUS 字符串，并指示为 GUID 提供的数据类型： 

fNDIS_GUID_TO_OID  
如果设置，则指示 NDIS_GUID 结构将 GUID 映射到 OID。

fNDIS_GUID_TO_STATUS  
如果设置，则指示 NDIS_GUID 结构将 GUID 映射到 NDIS_STATUS 字符串。

fNDIS_GUID_ANSI_STRING  
如果设置，则指示为 GUID 提供了以 null 结尾的 ANSI 字符串。

fNDIS_GUID_UNICODE_STRING  
如果设置，则表示为 GUID 提供了 Unicode 字符串。

fNDIS_GUID_ARRAY  
如果设置，则指示为 GUID 提供数据项的数组。 指定的大小指示数组中每个数据项的长度。

fNDIS_GUID_ALLOW_READ  
如果设置，则表示允许所有用户查询此 GUID。

fNDIS_GUID_ALLOW_WRITE  
如果设置，则表示允许所有用户设置此 GUID。

## <a name="remarks"></a>备注

> [!NOTE]
> 默认情况下，只有具有管理员权限的用户才能访问微型端口驱动程序提供的自定义 WMI Guid。 如果微型端口驱动程序支持该 GUID 的读取或写入操作，则具有管理员权限的用户始终可以读取或写入自定义 GUID。 设置 fNDIS_GUID_ALLOW_READ 和 fNDIS_GUID_ALLOW_WRITE 标志，以允许所有用户访问自定义 GUID。

请注意，微型端口驱动程序注册的所有自定义 Guid 必须设置 fNDIS_GUID_TO_OID 或 fNDIS_GUID_TO_STATUS （绝不会设置两者）。 所有其他标志可以通过使用 OR 运算符（如果适用）组合在一起。

在下面的示例中，NDIS_GUID 结构将 GUID 映射到 OID_GEN_CO_RCV_PDUS_NO_BUFFER：

```cpp 
NDIS_GUID NdisGuid =  {{0x0a214809, 0xe35f, 0x11d0, 0x96, 0x92, 0x00,
 0xc0, 0x4f, 0xc3, 0x35, 0x8c},
 GUID_NDIS_GEN_CO_RCV_PDUS_NO_BUFFER,
 OID_GEN_CO_RCV_PDUS_NO_BUFFER,
 4,
 fNDIS_GUID_TO_OID};
```
GUID 是 Windows Management Instrumentation （WMI）用于获取或设置信息的标识符。 NDIS 截获 WMI 发送到 NDIS 驱动程序的 GUID，将 GUID 映射到 OID，并将 OID 发送到该驱动程序。 驱动程序将数据项返回到 NDIS，然后将数据返回到 WMI。

NDIS 还会将 NIC 状态的更改转换为 WMI 识别的 Guid。 当微型端口驱动程序报告 NIC 状态与[NdisMCoIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)的更改时，ndis 会将微型端口驱动程序指示的 NDIS_STATUS 转换为 NDIS 发送到 WMI 的 GUID。

如果面向连接的微型端口驱动程序支持海关 Guid，则它必须支持 OID_GEN_CO_SUPPORTED_GUIDS，这将返回到 NDIS，以将自定义 Guid 映射到自定义 Oid 或 NDIS_STATUS 字符串。 通过 OID_GEN_CO_SUPPORTED_GUIDS 查询微型端口驱动程序之后，NDIS 会将微型端口驱动程序的自定义 Guid 注册到 WMI。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

