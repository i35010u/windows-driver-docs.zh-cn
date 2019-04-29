---
title: OID_CO_TAPI_LINE_CAPS
description: 本主题介绍 OID_CO_TAPI_LINE_CAPS 对象标识符 (OID)。
ms.assetid: 82c2bcb4-fb58-4e14-b1d4-2bcc0c4fcd1d
keywords:
- OID_CO_TAPI_LINE_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: c55b4c15b07c41afa7fe7f05b979cb921aad7e94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380709"
---
# <a name="oidcotapilinecaps"></a>OID_CO_TAPI_LINE_CAPS

OID_CO_TAPI_LINE_CAPS OID 请求呼叫管理器或集成的微型端口调用管理器 (MCM) 驱动程序返回指定行的电话服务功能。 此 OID 还会请求呼叫管理器或 MCM 驱动程序，以指示该线路上的地址是否具有不同的电话服务功能。

此请求使用 CO_TAPI_LINE_CAPS 结构，定义，如下所示，若要查询的指定行的电话服务功能：

```c++
typedef struct _CO_TAPI_LINE_CAPS {
    IN  ULONG           ulLineID;
    OUT ULONG           ulFlags;
    OUT LINE_DEV_CAPS   LineDevCaps;
} CO_TAPI_LINE_CAPS, *PCO_TAPI_LINE_CAPS;
``` 

此结构的成员包含下列信息：

**ulLineID**  
指定功能应为哪个电话服务返回的行。 **ulLineID**是从零开始的标识符。

**ulFlags**  
如果在行支持具有不同的电话服务功能的多个地址，呼叫管理器或 MCM 驱动程序设置位 ulFlags; CO_TAPI_FLAG_PER_ADDRESS_CAPS否则，呼叫管理器或 MCM 驱动程序将清除此位。 未定义的所有位保留，必须设置为 0。

**LineDevCaps**  
指定行中，格式为 LINE_DEV_CAPS 结构的电话服务功能。 有关此结构的详细信息，请参阅 Microsoft Windows SDK 和 ndistapi.h 标头文件。

## <a name="remarks"></a>备注

查询与呼叫管理器或 MCM 驱动程序的设备的电话服务功能后[OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md)，面向连接的客户端查询的相应行设备支持的电话服务功能。

- 如果设备支持的所有行都具有相同的行功能，并且这些行中的所有地址都具有相同的地址功能，客户端会查询一次 OID_CO_TAPI_LINE_CAPS 若要获取设备的行功能。 在这种情况下，行功能返回的呼叫管理器或 MCM 驱动程序将应用到设备支持的所有行。
- 如果设备支持多行使用不同的功能，但是，并且/或者如果这些行上的地址具有不同的地址的功能，客户端会查询 OID_CO_TAPI_LINE_CAPS 一次为设备获取功能支持的每个行每个行。

**UlFlags**设置确定多少次客户端随后会查询在行上的地址的功能：

- 如果命令行支持只能有一个地址，或者命令行支持具有相同的地址功能的多个地址，客户端会查询一次 OID_CO_TAPI_ADDRESS_CAPS。
- 如果在行支持具有不同功能的多个地址，客户端必须查询 OID_CO_TAPI_ADDRESS_CAPS 一次每个地址在行上。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

