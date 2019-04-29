---
title: OID_CO_TAPI_CM_CAPS
description: 本主题介绍 OID_CO_TAPI_CM_CAPS 对象标识符 (OID)。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_CM_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc20e53411e46cf75a3e86d44b7f63a4d1f4c24f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380711"
---
# <a name="oidcotapicmcaps"></a>OID_CO_TAPI_CM_CAPS

OID_CO_TAPI_CM_CAPS OID 请求呼叫管理器或集成的微型端口调用管理器 (MCM) 驱动程序返回其设备支持的行数 （它提供了调用管理服务的设备）。 此 OID 还会请求呼叫管理器或 MCM 驱动程序，以指示这些行是否具有不同的行的功能。

此请求使用 CO_TAPI_CM_CAPS 结构，其定义，如下所示：

```c++
typedef struct _CO_TAPI_CM_CAPS {
    OUT ULONG   ulCoTapiVersion;
    OUT ULONG   ulNumLines;
    OUT ULONG   ulFlags;
} CO_TAPI_CM_CAPS, *PCO_TAPI_CM_CAPS;
``` 

此结构的成员包含下列信息：

**ulCoTapiVersion**  
指定支持的呼叫管理器或 MCM 驱动程序的 TAPI 版本。 呼叫管理器或 MCM 驱动程序应设置为 CO_TAPI_VERSION。

**ulNumLines**  
指定设备支持的行的数。

**ulFlags**  
如果设备支持具有不同的行的功能的多个行，或者如果任何这些行上的地址具有不同的地址的功能，呼叫管理器或 MCM 驱动程序设置中的位 CO_TAPI_FLAG_PER_LINE_CAPS **ulFlags**;否则，呼叫管理器或 MCM 驱动程序将清除此位。 未定义的所有位保留供将来使用，必须设置为 0。

## <a name="remarks"></a>备注

面向连接的客户端使用此 OID 从返回的信息来确定如何，它将查询与呼叫管理器或 MCM 驱动程序的设备的行功能[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

