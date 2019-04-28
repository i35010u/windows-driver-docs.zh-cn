---
title: OID_TCP_CONNECTION_OFFLOAD_PARAMETERS
description: 本主题介绍 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS 对象标识符 (OID)。
ms.assetid: 6481D565-900A-4B75-A60F-72701FB45FAD
keywords:
- OID_TCP_CONNECTION_OFFLOAD_PARAMETERS，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29f5a500a249237ce22a4205f7f5c010ab9189b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331809"
---
# <a name="oidtcpconnectionoffloadparameters"></a>OID_TCP_CONNECTION_OFFLOAD_PARAMETERS

作为查询请求，过量驱动程序可以使用 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID 以确定基础的微型端口适配器的当前连接卸载设置。 NDIS 处理此 OID 查询的微型端口驱动程序。

作为 set 请求，NDIS 和过量驱动程序使用 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID，若要设置连接将卸载基础的微型端口适配器的配置的参数。 支持连接卸载的微型端口驱动程序必须处理此 OID 集请求。 否则，OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID 是可选的微型端口驱动程序。

## <a name="remarks"></a>备注

**InformationBuffer**的成员[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[NDIS_TCP_CONNECTION_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff567876)结构。

> [!NOTE]
> 不要混淆与 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID 管理应用程序用来启用或禁用 TCP 卸载功能。

### <a name="see-also"></a>请参阅

[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

