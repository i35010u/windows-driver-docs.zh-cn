---
title: OID_CO_TAPI_ADDRESS_CAPS
description: 本主题介绍 OID_CO_TAPI_ADDRESS_CAPS 对象标识符 (OID)。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_ADDRESS_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 136a7b1a892e817cff0c6acd1a5a13fd01624c87
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380713"
---
# <a name="oidcotapiaddresscaps"></a>OID_CO_TAPI_ADDRESS_CAPS

OID_CO_TAPI_ADDRESS_CAPS OID 请求呼叫管理器或集成的微型端口调用管理器 (MCM) 驱动程序，以返回在指定的行上指定的地址的电话服务功能。

此请求使用 CO_TAPI_ADDRESS_CAPS 结构，其定义，如下所示：

```c++
typedef struct _CO_TAPI_ADDRESS_CAPS {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    OUT ULONG               ulFlags;
    OUT LINE_ADDRESS_CAPS   LineAddressCaps;
} CO_TAPI_ADDRESS_CAPS, *PCO_TAPI_ADDRESS_CAPS;
``` 

此结构的成员包含下列信息：

**ulLineID**  
指定给定的地址所在的行的从零开始的行标识符。

**ulAddressID**  
应为其返回功能在行上指定的从零开始的地址标识符。

**ulFlags**  
这些标志将保留。

**LineAddressCaps**  
指定的地址，格式为 LINE_ADDRESS_CAPS 结构的电话服务功能。 有关此结构的详细信息，请参阅 Microsoft Windows SDK 和 ndistapi.h 标头文件。

## <a name="remarks"></a>备注

查询使用的呼叫管理器或 MCM 驱动程序的设备的行功能后[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)，面向连接的客户端查询每个行的地址的功能，如下所示：

- 如果前面的查询的 OID_CO_TAPI_LINE_CAPS 指示行支持只能有一个地址，或在行上的所有地址都具有相同的地址功能，客户端会查询一次 OID_CO_TAPI_ADDRESS_CAPS 来确定所有的功能在行上的地址。 在这种情况下，地址功能返回的呼叫管理器或 MCM 驱动程序将应用于在行上的所有地址。

- 如果命令行支持具有不同功能的多个地址，客户端会查询 OID_CO_TAPI_ADDRESS_CAPS 一次为每个地址在行上。 在这种情况下，地址功能返回的呼叫管理器或 MCM 驱动程序将应用于指定的行上指定的地址。

呼叫管理器或 MCM 驱动程序返回在指定的地址的地址功能**LineAddressCaps**。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

