---
title: OID_TCP_OFFLOAD_CURRENT_CONFIG
description: 本主题介绍 OID_TCP_OFFLOAD_CURRENT_CONFIG 对象标识符 (OID)。
ms.assetid: 8DC81A41-1E4D-4F78-80D1-54C79F974CE3
keywords:
- OID_TCP_OFFLOAD_CURRENT_CONFIG，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7472dc34fec0c8c2f14e252d6d262efc7d1c36e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354154"
---
# <a name="oidtcpoffloadcurrentconfig"></a>OID_TCP_OFFLOAD_CURRENT_CONFIG

作为查询请求，管理应用程序 （或可能是基础驱动程序） 使用 OID_TCP_OFFLOAD_CURRENT_CONFIG OID 来确定基础的微型端口适配器的当前任务卸载配置设置。 通过 Microsoft Windows Management Instrumentation (WMI) 界面，系统管理员可以使用此 OID。

不支持组的请求。

## <a name="remarks"></a>备注

NDIS 处理此 OID 的微型端口驱动程序。 微型端口驱动程序报告到 NDIS 微型端口适配器卸载功能。 有关传递任务的信息的卸载配置设置到 NDIS 从微型端口驱动程序和 NDIS 到过量驱动程序，请参阅 NDIS_OFFLOAD。

**InformationBuffer**的成员[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构。 **NDIS_OFFLOAD**结构包括以下功能，微型端口适配器：

- 标头信息，其中包括任务卸载版本。
- 校验和卸载的信息，在[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567878)结构。
- 大型将卸载版本 1 (LSOV1) 发送信息，请在[NDIS_TCP_LARGE_SEND_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff567883)结构。
- Internet 协议安全 (IPsec) 信息中[NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)结构。
- 大型将卸载版本 2 (LSOV2) 发送信息，请在[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://msdn.microsoft.com/library/windows/hardware/ff567884)结构。

OID_TCP_OFFLOAD_CURRENT_CONFIG，响应**封装**上述列表中的结构的成员定义的微型端口适配器的数据包封装功能。 NDIS 提供中提供的标志的按位 OR**封装**的这些结构的成员。 其他结构成员包含各种卸载服务的设置。 有关封装和其他功能的详细信息，请参阅[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567878)， [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff567883)， [NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)，并[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://msdn.microsoft.com/library/windows/hardware/ff567884)。

微型端口适配器必须支持以太网的所有类型的任务封装卸载它们支持。 其他类型是封装的可选的。

微型端口驱动程序自动应启用所有任务卸载功能在初始化过程。

### <a name="see-also"></a>请参阅

[NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)  
[NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)  
[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)  
[NDIS_TCP_IP_CHECKSUM_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567878)  
[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](https://msdn.microsoft.com/library/windows/hardware/ff567884)    
[NDIS_IPSEC_OFFLOAD_V1](https://msdn.microsoft.com/library/windows/hardware/ff565796)  

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

