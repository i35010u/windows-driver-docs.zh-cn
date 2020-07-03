---
title: OID_CO_TAPI_LINE_CAPS
description: 本主题介绍 OID_CO_TAPI_LINE_CAPS 对象标识符（OID）。
ms.assetid: 82c2bcb4-fb58-4e14-b1d4-2bcc0c4fcd1d
keywords:
- OID_CO_TAPI_LINE_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01cea4126ec7f85cd84e6ac215af06a0f28dae9e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917523"
---
# <a name="oid_co_tapi_line_caps"></a>OID_CO_TAPI_LINE_CAPS

OID_CO_TAPI_LINE_CAPS OID 请求调用管理器或集成微型端口调用管理器（MCM）驱动程序返回指定行的电话功能。 此 OID 还请求调用管理器或 MCM 驱动程序，以指示此行上的地址是否具有不同的电话服务功能。

此请求使用如下定义的 CO_TAPI_LINE_CAPS 结构来查询指定行的电话服务功能：

```c++
typedef struct _CO_TAPI_LINE_CAPS {
    IN  ULONG           ulLineID;
    OUT ULONG           ulFlags;
    OUT LINE_DEV_CAPS   LineDevCaps;
} CO_TAPI_LINE_CAPS, *PCO_TAPI_LINE_CAPS;
``` 

此结构的成员包含以下信息：

**ulLineID**  
指定应返回其电话功能的行。 **ulLineID**是从零开始的标识符。

**ulFlags**  
如果行支持具有不同电话功能的多个地址，则调用管理器或 MCM 驱动程序会在 ulFlags 中设置 CO_TAPI_FLAG_PER_ADDRESS_CAPS 位;否则，调用管理器或 MCM 驱动程序将清除此位。 所有未定义的位均保留，并且必须设置为0。

**LineDevCaps**  
指定行的电话服务功能，格式为 LINE_DEV_CAPS 结构。 有关此结构的详细信息，请参阅 Microsoft Windows SDK 和 ndistapi 头文件。

## <a name="remarks"></a>备注

使用[OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md)查询呼叫管理器或 MCM 驱动程序的设备的电话功能后，面向连接的客户端将查询设备支持的线路的电话功能。

- 如果设备支持的所有行都具有相同的线路功能，并且这些线路上的所有地址都具有相同的地址功能，则客户端查询 OID_CO_TAPI_LINE_CAPS 一次，以获取设备的线路功能。 在这种情况下，由呼叫管理器或 MCM 驱动程序返回的线路功能适用于设备支持的所有线路。
- 但是，如果设备支持多个具有不同功能的行，并且/或者这些线路上的地址具有不同的地址功能，则客户端将在每行支持的每行中查询一次 OID_CO_TAPI_LINE_CAPS，以获取每行的功能。

**UlFlags**设置确定客户端随后查询行中地址的功能的次数：

- 如果行仅支持一个地址，或者行支持多个具有相同地址功能的地址，则客户端将 OID_CO_TAPI_ADDRESS_CAPS 一次。
- 如果行支持具有不同功能的多个地址，则客户端必须针对行中的每个地址查询一次 OID_CO_TAPI_ADDRESS_CAPS。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

