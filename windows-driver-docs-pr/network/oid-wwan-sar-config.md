---
title: OID_WWAN_SAR_CONFIG
description: OID_WWAN_SAR_CONFIG 获取或设置有关移动宽带 (MB 的信息) 设备特定的吸收速率 (SAR) 后退模式和级别。
ms.assetid: 78B049E0-A80E-42AA-9D81-D45BBCF84FCB
ms.date: 08/17/2018
keywords: -从 Windows Vista 开始 OID_WWAN_SAR_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c3b75c85179ac9f3f6a64254778f5c6096480b58
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811983"
---
# <a name="oid_wwan_sar_config"></a>OID_WWAN_SAR_CONFIG

OID_WWAN_SAR_CONFIG 获取或设置有关移动宽带 (MB 的信息) 设备特定的吸收速率 (SAR) 后退模式和级别。 

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送 [NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md) 状态通知，其中包含描述当前 SAR 配置的 [**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info) 结构。

对于 Set 请求，此 OID 的负载包含一个 [**NDIS_WWAN_SET_SAR_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config) 结构，该结构指定调制解调器的新 SAR 配置。

## <a name="remarks"></a>备注

完成每个查询或设置请求后，微型端口驱动程序应返回 [**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info) 结构，该结构包含设备上与移动宽带关联的所有天线的信息。

有关使用此 OID 的详细信息，请参阅 [MBIM_CID_MS_SAR_CONFIG](./mb-sar-platform-support.md#mbim_cid_ms_sar_config)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[MB SAR 平台支持](./mb-sar-platform-support.md)

[NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)

[**NDIS_WWAN_SET_SAR_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)