---
title: OID_WWAN_MPDP
description: OID_WWAN_MPDP 设置或查询表示主 PDP 上下文/EPS 持有者的 MB 设备的多个数据包数据协议 (MPDP) 接口的信息。
ms.assetid: 2A8E496A-212A-4999-A82C-9B97CEEC2C7E
keywords:
- OID_WWAN_MPDP、 MPDP OID
ms.date: 06/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: 757b96d735e332cdbf265fd5b37f8515133b2bc7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527178"
---
# <a name="oidwwanmpdp"></a>OID_WWAN_MPDP

OID_WWAN_MPDP 设置或查询表示主 PDP 上下文/EPS 持有者的 MB 设备的多个数据包数据协议 (MPDP) 接口的信息。

对于查询请求，微型端口驱动程序响应 MB 服务以异步方式通过最初返回 NDIS_STATUS_INDICATION_REQUIRED。 查询请求完成后，该驱动程序会发送[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)包含一系列主要 PDP 上下文中，子接口的通知格式[ **NDIS_WWAN_MPDP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)结构。

对于组的请求，如查询请求与微型端口驱动程序响应 MB 服务以异步方式通过最初返回 NDIS_STATUS_INDICATION_REQUIRED。 设置请求包含[ **NDIS_WWAN_SET_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)结构，其中又包含[ **NDIS_WWAN_MPDP_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)具有操作信息的结构。 

如果**操作**的成员**NDIS_WWAN_MPDP_INFO**结构设置为**WwanMPDPOperationCreateChildInterface**，客户端驱动程序会创建一个新的子接口主 PDP 上下文。 此操作，以及如果操作成功，新创建的子接口的 GUID 的状态结果返回到中的 MB 服务[ **NDIS_WWAN_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)结构中包含[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知。

如果**操作**的成员**NDIS_WWAN_MPDP_INFO**结构设置为**WwanMPDPOperationDeleteChildInterface**，微型端口驱动程序中删除相应的以前创建和删除操作的相关信息返回到中的 MB 服务的子接口[ **NDIS_WWAN_MPDP_STATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)结构中包含[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)通知。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1809 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>另请参阅

[NDIS_STATUS_WWAN_MPDP_LIST](ndis-status-wwan-mpdp-list.md)

[**NDIS_WWAN_MPDP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_list)

[**NDIS_WWAN_SET_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_mpdp_state)

[**NDIS_WWAN_MPDP_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_info)

[NDIS_STATUS_WWAN_MPDP_STATE](ndis-status-wwan-mpdp-state.md)

[**NDIS_WWAN_MPDP_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_mpdp_state)

[*EvtMbbDeviceCreateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter)
