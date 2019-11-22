---
title: OID_WWAN_LTE_ATTACH_CONFIG
description: OID_WWAN_LTE_ATTACH_CONFIG 允许操作系统查询或设置插入的 SIM 提供程序的默认 LTE 附加上下文（MCC/MNC 对）。
ms.assetid: 7E753513-D6A2-4B67-9AED-83A695C39D3C
ms.date: 08/22/2018
keywords: -从 Windows Vista 开始 OID_WWAN_LTE_ATTACH_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bb13251a5d2ad8efaffb48de3995b640e19d1fc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843840"
---
# <a name="oid_wwan_lte_attach_config"></a>OID_WWAN_LTE_ATTACH_CONFIG

OID_WWAN_LTE_ATTACH_CONFIG 允许操作系统查询或设置插入的 SIM 提供程序的默认 LTE 附加上下文（MCC/MNC 对）。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)状态通知，其中包含描述 LTE 附加配置的[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)结构。

对于 Set 请求，此 OID 的负载包含一个[**NDIS_WWAN_SET_LTE_ATTACH_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)结构，该结构描述了要设置的调制解调器的 LTE 附加上下文信息。

## <a name="remarks"></a>备注

完成每个查询或设置请求后，微型端口驱动程序应返回描述 LTE 附加配置的[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)通知。

有关使用此 OID 的详细信息，请参阅[MBIM_CID_MS_LTE_ATTACH_CONFIG](mb-lte-attach-operations.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1703 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG](ndis-status-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)

[**NDIS_WWAN_SET_LTE_ATTACH_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_lte_attach_context)
