---
title: OID_CO_TAPI_CM_CAPS
description: 本主题介绍) OID_CO_TAPI_CM_CAPS 对象标识符 (OID。
keywords:
- OID_CO_TAPI_CM_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1296f5542beeda704a61d80147e8445c11afeae6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828455"
---
# <a name="oid_co_tapi_cm_caps"></a>OID_CO_TAPI_CM_CAPS

OID_CO_TAPI_CM_CAPS OID 请求呼叫管理器或集成微型端口调用管理器 (MCM) 驱动程序返回其设备所支持的行数 (为其提供呼叫管理服务) 的设备。 此 OID 还请求调用管理器或 MCM 驱动程序指示这些行是否具有不同的线功能。

此请求使用 CO_TAPI_CM_CAPS 结构，定义如下：

```c++
typedef struct _CO_TAPI_CM_CAPS {
    OUT ULONG   ulCoTapiVersion;
    OUT ULONG   ulNumLines;
    OUT ULONG   ulFlags;
} CO_TAPI_CM_CAPS, *PCO_TAPI_CM_CAPS;
``` 

此结构的成员包含以下信息：

**ulCoTapiVersion**  
指定呼叫管理器或 MCM 驱动程序支持的 TAPI 版本。 调用管理器或 MCM 驱动程序应将此设置为 CO_TAPI_VERSION。

**ulNumLines**  
指定设备支持的行数。

**ulFlags**  
如果设备支持多个具有不同线路功能的线路，或者任何这些线路上的地址具有不同的地址功能，则调用管理器或 MCM 驱动程序会在 **ulFlags** 中设置 CO_TAPI_FLAG_PER_LINE_CAPS 位;否则，调用管理器或 MCM 驱动程序将清除此位。 所有未定义的位将保留以供将来使用，并且必须设置为0。

## <a name="remarks"></a>备注

面向连接的客户端使用从此 OID 返回的信息来确定它将如何使用 [OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)查询调用管理器或 MCM 驱动程序的设备的行功能。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

