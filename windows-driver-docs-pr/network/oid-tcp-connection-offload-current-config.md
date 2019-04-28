---
title: OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG
description: 本主题介绍 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG 对象标识符 (OID)。
ms.assetid: 29CB74B1-8D7F-4EC2-AAAC-93D454824031
keywords:
- OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a02d0bde9107284dccdec13092bdf818840a74c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331813"
---
# <a name="oidtcpconnectionoffloadcurrentconfig"></a>OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG

作为查询请求，管理应用程序 （或可能过量的驱动程序） 可以使用 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG OID 来确定当前已启用连接卸载功能的基础的微型端口适配器。 通过 Microsoft Windows Management Instrumentation (WMI) 界面，系统管理员可以使用此 OID。

不支持组的请求。

## <a name="remarks"></a>备注

NDIS 处理此 OID 的微型端口驱动程序。 微型端口驱动程序报告微型端口适配器连接到 NDIS 的卸载设置。 有关连接卸载配置将设置传递到 NDIS 从微型端口驱动程序和 NDIS 给基础驱动程序的信息，请参阅[NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)。

**InformationBuffer**的成员[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)结构。

OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG，响应**封装**NDIS_TCP_CONNECTION_OFFLOAD 成员定义的微型端口适配器当前的数据包封装配置。 NDIS 提供中提供的标志的按位 OR**封装**成员。 NDIS_TCP_CONNECTION_OFFLOAD 的其他成员包含各种连接卸载服务的设置。 有关封装和其他功能的详细信息，请参阅[NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)并[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)。


### <a name="see-also"></a>请参阅

[NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567875)

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

