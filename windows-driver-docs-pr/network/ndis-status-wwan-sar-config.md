---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_CONFIG 通知来通知关于完成的上一个 OID_WWAN_SAR_CONFIG 查询或一组请求的移动宽带 (MB) 服务。
ms.assetid: 50DAEFAB-E86A-41EA-A237-802AD8F83BB2
ms.date: 08/17/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SAR_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5c4932270c9831ef9ecfd379c04e2278f1200db0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569410"
---
# <a name="ndisstatuswwansarconfig"></a>NDIS_STATUS_WWAN_SAR_CONFIG

微型端口驱动程序使用**NDIS_STATUS_WWAN_SAR_CONFIG**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)查询或设置请求。

未经请求的事件不适用。

使用此通知[ **NDIS_WWAN_SAR_CONFIG_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1703 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB 特别行政区平台支持](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)
