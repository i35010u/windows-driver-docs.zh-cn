---
title: OID_CO_TAPI_ADDRESS_CAPS
description: 本主题介绍 OID_CO_TAPI_ADDRESS_CAPS 对象标识符（OID）。
ms.assetid: c0e44c1b-89d1-4c50-a1fc-8322bb1d00c2
keywords:
- OID_CO_TAPI_ADDRESS_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38825b1c6bb8e5e95e48a332dc68c5c71ae94e31
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916803"
---
# <a name="oid_co_tapi_address_caps"></a>OID_CO_TAPI_ADDRESS_CAPS

OID_CO_TAPI_ADDRESS_CAPS OID 请求呼叫管理器或集成微型端口调用管理器（MCM）驱动程序返回指定行上指定地址的电话服务功能。

此请求使用 CO_TAPI_ADDRESS_CAPS 结构，定义如下：

```c++
typedef struct _CO_TAPI_ADDRESS_CAPS {
    IN  ULONG               ulLineID;
    IN  ULONG               ulAddressID;
    OUT ULONG               ulFlags;
    OUT LINE_ADDRESS_CAPS   LineAddressCaps;
} CO_TAPI_ADDRESS_CAPS, *PCO_TAPI_ADDRESS_CAPS;
``` 

此结构的成员包含以下信息：

**ulLineID**  
指定给定地址所在行的从零开始的行标识符。

**ulAddressID**  
指定应返回其功能的行的从零开始的地址标识符。

**ulFlags**  
保留这些标志。

**LineAddressCaps**  
指定地址的电话服务功能，格式为 LINE_ADDRESS_CAPS 结构。 有关此结构的详细信息，请参阅 Microsoft Windows SDK 和 ndistapi 头文件。

## <a name="remarks"></a>备注

使用[OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md)查询呼叫管理器或 MCM 驱动程序的设备的线路功能后，面向连接的客户端将查询每行的地址的功能，如下所示：

- 如果 OID_CO_TAPI_LINE_CAPS 的上一个查询指出该行仅支持一个地址，或者该行上的所有地址都具有相同的地址功能，则客户端将 OID_CO_TAPI_ADDRESS_CAPS 一次来确定该行上所有地址的功能。 在这种情况下，调用管理器或 MCM 驱动程序返回的地址功能适用于行中的所有地址。

- 如果某行支持具有不同功能的多个地址，则客户端将对该行上的每个地址 OID_CO_TAPI_ADDRESS_CAPS 一次。 在这种情况下，调用管理器或 MCM 驱动程序返回的地址功能适用于指定的行上的指定地址。

调用管理器或 MCM 驱动程序返回**LineAddressCaps**中指定地址的地址功能。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

