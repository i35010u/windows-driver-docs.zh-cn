---
title: OID_GEN_CO_SUPPORTED_GUIDS
description: 本主题介绍 OID_GEN_CO_SUPPORTED_GUIDS 对象标识符 (OID)。
ms.assetid: d82d6ecb-f70b-4fc2-97eb-331aafe1fe57
keywords:
- OID_GEN_CO_SUPPORTED_GUIDS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea1973c4261a10a61ceb2c16bd489bd1c894c08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386220"
---
# <a name="oidgencosupportedguids"></a>OID_GEN_CO_SUPPORTED_GUIDS

OID_GEN_CO_SUPPORTED_GUIDS OID 请求微型端口驱动程序，以返回类型 NDIS_GUID 的结构数组。 数组中的每个结构指定的映射的自定义 GUID （全局唯一标识符） 是一个自定义的 OID 或微型端口驱动程序将通过发送 NDIS_STATUS [NdisMCoIndicateStatusEx](https://msdn.microsoft.com/library/windows/hardware/ff563562)。

NDIS_GUID 结构定义，如下所示：

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

此结构的成员包含下列信息：

**guid**  
为微型端口驱动程序定义自定义 GUID。

**oid**  
向其自定义 OID **Guid**映射。

**状态**  
向其 NDIS_STATUS **Guid**映射。

**大小**  
设置 fNDIS_GUID_ARRAY 标志后，**大小**以字节为单位的微型端口驱动程序返回的数组中每个数据项中指定的大小。 如果设置了 fNDIS_GUID_ANSI_STRING 或 fNDIS_GUID_NDIS_STRING 标志，**大小**设置为-1。 否则为**大小**以字节为单位的 GUID 表示的数据项中指定的大小。

**标志**  
以下标志可以是或运算到一起以指示 GUID 映射到 OID 或 NDIS_STATUS 字符串，还可以指示提供的 guid 的数据类型： 

fNDIS_GUID_TO_OID  
设置时，指示 NDIS_GUID 结构映射到一个 OID 为 GUID。

fNDIS_GUID_TO_STATUS  
设置时，指示 NDIS_GUID 结构映射到 NDIS_STATUS 字符串 GUID。

fNDIS_GUID_ANSI_STRING  
设置时，指示以 null 结尾的 ANSI 字符串提供的 guid。

fNDIS_GUID_UNICODE_STRING  
设置时，指示 Unicode 字符串，提供的 guid。

fNDIS_GUID_ARRAY  
设置时，指示这些 guid 提供数据项的数组。 指定的大小指示数组中每个数据项的长度。

fNDIS_GUID_ALLOW_READ  
设置时，指示允许所有用户来查询此 GUID。

fNDIS_GUID_ALLOW_WRITE  
设置时，指示将允许所有用户设置此 GUID。

## <a name="remarks"></a>备注

> [!NOTE]
> 默认情况下，仅具有管理员权限的用户可以访问由微型端口驱动程序提供的自定义 WMI Guid。 具有管理员权限的用户始终可以读取或写入一个自定义 GUID，如果微型端口驱动程序支持读取或写入该 GUID 的操作。 设置 fNDIS_GUID_ALLOW_READ 和 fNDIS_GUID_ALLOW_WRITE 标志，以允许所有用户访问自定义 GUID。

请注意，所有自定义 Guid 注册的微型端口驱动程序必须设置 fNDIS_GUID_TO_OID 或 fNDIS_GUID_TO_STATUS （永远不会同时设置）。 所有其他标志可能会根据使用 OR 运算符组合。

在以下示例中，NDIS_GUID 结构将 GUID 映射到 OID_GEN_CO_RCV_PDUS_NO_BUFFER:

```cpp 
NDIS_GUID NdisGuid =  {{0x0a214809, 0xe35f, 0x11d0, 0x96, 0x92, 0x00,
 0xc0, 0x4f, 0xc3, 0x35, 0x8c},
 GUID_NDIS_GEN_CO_RCV_PDUS_NO_BUFFER,
 OID_GEN_CO_RCV_PDUS_NO_BUFFER,
 4,
 fNDIS_GUID_TO_OID};
```
GUID 是通过 Windows Management Instrumentation (WMI) 用于获取或设置信息的标识符。 NDIS 截获由 WMI 发送到 NDIS 驱动程序的 GUID，将 GUID 映射到 OID，并向驱动程序发送 OID。 驱动程序将返回到 NDIS，然后将数据返回到 WMI 数据项目。

NDIS 还将通过 WMI 识别的 Guid 转换为 NIC 状态变化。 当微型端口驱动程序报告了与 NIC 状态中的更改[NdisMCoIndicateStatusEx](https://msdn.microsoft.com/library/windows/hardware/ff563562)，NDIS 转换为由到 NDIS 将发送到 WMI 的 GUID 的微型端口驱动程序 NDIS_STATUS。

如果有面向连接的微型端口驱动程序支持海关 Guid，它必须支持 OID_GEN_CO_SUPPORTED_GUIDS，返回到 NDIS 映射到自定义 Oid 或 NDIS_STATUS 字符串的自定义 Guid。 查询与 OID_GEN_CO_SUPPORTED_GUIDS 微型端口驱动程序后, NDIS 向 WMI 注册微型端口驱动程序的自定义 Guid。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

