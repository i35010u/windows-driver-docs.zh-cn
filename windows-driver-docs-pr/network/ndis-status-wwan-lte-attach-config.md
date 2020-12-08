---
title: NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_LTE_ATTACH_CONFIG 查询或设置请求的完成有关。
ms.date: 08/22/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b5b875cd869438727ce59f93978bba545bbff525
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822917"
---
# <a name="ndis_status_wwan_lte_attach_config"></a>NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG

微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md) 查询或设置请求的完成有关。

如果网络通过无线 (OTA) 或短消息服务 (SMS) 更新了默认 LTE 附加上下文，则会发送未经请求的事件。 在这种情况下，微型端口驱动程序必须更新默认的 LTE 附加上下文，并将此通知发送到带有更新列表的主机操作系统。

此状态通知使用 [**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)
