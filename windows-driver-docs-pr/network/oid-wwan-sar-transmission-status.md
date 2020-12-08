---
title: OID_WWAN_SAR_TRANSMISSION_STATUS
description: OID_WWAN_SAR_TRANSMISSION_STATUS 根据特定的吸收速率 (SAR) 传输状态，启用或禁用从移动宽带 (MB) 调制解调器发出的通知。
ms.date: 08/20/2018
keywords: -从 Windows Vista 开始 OID_WWAN_SAR_TRANSMISSION_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 50c52a760a681e27708076982541ecfd070162fd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812931"
---
# <a name="oid_wwan_sar_transmission_status"></a>OID_WWAN_SAR_TRANSMISSION_STATUS

OID_WWAN_SAR_TRANSMISSION_STATUS 根据特定的吸收速率 (SAR) 传输状态，启用或禁用从移动宽带 (MB) 调制解调器发出的通知。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送 [NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md) 状态通知，其中包含描述是否在调制解调器中启用了 SAR 传输状态通知的 [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info) 结构。

对于 Set 请求，此 OID 的负载包含一个 [**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status) 结构，该结构指定是否应启用或禁用 SAR 传输状态通知。

## <a name="remarks"></a>备注

完成每个查询或设置请求后，微型端口驱动程序应返回一个 [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info) 结构，该结构描述是否在调制解调器中启用了有关传输状态的 SAR 通知。

有关使用此 OID 的详细信息，请参阅 [MBIM_CID_MS_TRANSMISSION_STATUS](./mb-sar-platform-support.md#mbim_cid_ms_transmission_status)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB SAR 平台支持](./mb-sar-platform-support.md)

[NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS](ndis-status-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)

[**NDIS_WWAN_SET_SAR_TRANSMISSION_STATUS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_transmission_status)
