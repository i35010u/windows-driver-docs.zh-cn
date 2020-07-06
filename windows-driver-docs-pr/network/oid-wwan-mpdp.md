---
title: OID_WWAN_MPDP
description: OID_WWAN_MPDP 为表示主 PDP 上下文/EPS 持有者的 MB 设备设置或查询有关多个数据包数据协议（MPDP）接口的信息。
ms.assetid: 2A8E496A-212A-4999-A82C-9B97CEEC2C7E
keywords:
- OID_WWAN_MPDP，MPDP OID
ms.date: 06/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 164d47ef3c906481b9dc29e0068d3f80249e0676
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968306"
---
# <a name="oid_wwan_mpdp"></a>OID_WWAN_MPDP

OID_WWAN_MPDP 为表示主 PDP 上下文/EPS 持有者的 MB 设备设置或查询有关多个数据包数据协议（MPDP）接口的信息。

对于查询请求，微型端口驱动程序通过最初返回 NDIS_STATUS_INDICATION_REQUIRED 来异步响应 MB 服务。 查询请求完成后，驱动程序将发送一个[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)通知，其中包含主 PDP 上下文的子接口列表，格式为[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)结构。

对于 set 请求，如使用 query 请求，微型端口驱动程序通过最初返回 NDIS_STATUS_INDICATION_REQUIRED 来异步响应 MB 服务。 设置请求包含[**NDIS_WWAN_SET_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)结构，后者又包含包含操作信息的[**NDIS_WWAN_MPDP_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)结构。 

如果**NDIS_WWAN_MPDP_INFO**结构的**操作**成员设置为**WwanMPDPOperationCreateChildInterface**，则客户端驱动程序将为主 PDP 上下文创建新的子接口。 此操作的状态结果以及新创建的子接口的 GUID （如果操作成功）将返回到[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知中包含的[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)结构中的 MB 服务。

如果**NDIS_WWAN_MPDP_INFO**结构的**操作**成员设置为**WwanMPDPOperationDeleteChildInterface**，微型端口驱动程序将删除先前创建的相应子接口，并将有关删除操作的信息返回到[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知中包含的[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)结构中的 MB 服务。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本1809

**标头**： Ntddndis （包括 Ndis .h）


## <a name="see-also"></a>另请参阅

[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)

[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)

[**NDIS_WWAN_SET_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)

[**NDIS_WWAN_MPDP_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)

[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)

[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)

[*EvtMbbDeviceCreateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter)
