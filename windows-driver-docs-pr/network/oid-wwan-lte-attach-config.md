---
title: OID_WWAN_LTE_ATTACH_CONFIG
description: OID_WWAN_LTE_ATTACH_CONFIG 使查询操作系统，或设置默认 LTE 附加插入的 SIM 的提供程序 （MCC/mnc 对） 的上下文。
ms.assetid: 7E753513-D6A2-4B67-9AED-83A695C39D3C
ms.date: 08/22/2018
keywords: -从 Windows Vista 开始 OID_WWAN_LTE_ATTACH_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 157740fd5afd819823d8c015961595ac6ed8bec9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523922"
---
# <a name="oidwwanlteattachconfig"></a>OID_WWAN_LTE_ATTACH_CONFIG

OID_WWAN_LTE_ATTACH_CONFIG 使查询操作系统，或设置默认 LTE 附加插入的 SIM 的提供程序 （MCC/mnc 对） 的上下文。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)状态通知包含[ **NDIS_WWAN_LTE_ATTACH_CONTEXTS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)结构描述 LTE 附加配置。

对于组的请求，此 OID 负载包含[ **NDIS_WWAN_SET_LTE_ATTACH_CONTEXT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)结构描述 LTE 附加的调制解调器，若要设置的上下文信息。

## <a name="remarks"></a>备注

每个查询或一组请求后，微型端口驱动程序应返回[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)介绍 LTE 的通知连接配置。

有关使用此 OID 的详细信息，请参阅[MBIM_CID_MS_LTE_ATTACH_CONFIG](mb-lte-attach-operations.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1703 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>另请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)

[**NDIS_WWAN_SET_LTE_ATTACH_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)
