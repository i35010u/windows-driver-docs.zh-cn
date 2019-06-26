---
title: OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES
description: 本主题介绍 OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES 对象标识符 (OID)。
ms.assetid: 9958F93C-0D68-428B-A25C-7FF6E4F37702
keywords:
- OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ba72d60d8adc52b40dc97e2a752cd99535a8710
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386961"
---
# <a name="oidtcpoffloadhardwarecapabilities"></a>OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES

作为查询请求，OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES OID 报告任务卸载硬件功能的微型端口适配器的硬件。 用户模式应用程序 （或可能是基础驱动程序） 可以查询此 OID 来确定任务卸载硬件功能的基础的微型端口适配器。 系统管理员可以通过 Windows Management Instrumentation (WMI) 界面中使用此 OID。

不支持组的请求。

## <a name="remarks"></a>备注

NDIS 处理此 OID 的微型端口驱动程序。 微型端口驱动程序报告到 NDIS 微型端口适配器硬件功能。 有关报告任务卸载硬件功能到 NDIS 从微型端口驱动程序和 NDIS 基础驱动程序的信息，请参阅[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)。

**InformationBuffer**的成员[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。 NDIS 返回 NDIS_STATUS_BUFFER_TOO_SHORT 如果缓冲区不够大。

在确定微型端口适配器的硬件功能之后, 过量的应用程序或驱动程序可以使用[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) 情况为未启用OID以启用当前报告的功能[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md) OID。

### <a name="see-also"></a>请参阅

[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)  

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

