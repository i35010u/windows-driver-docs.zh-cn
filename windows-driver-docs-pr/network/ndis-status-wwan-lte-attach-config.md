---
title: NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知来通知关于完成的上一个 OID_WWAN_LTE_ATTACH_CONFIG 查询或一组请求的移动宽带 (MB) 服务。
ms.assetid: 866BCD4F-85A1-46C8-9FE2-8C5A8ADCD3CA
ms.date: 08/22/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 27af6dd461be18333b12119b7d5d9be8c31f05c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526844"
---
# <a name="ndisstatuswwanlteattachconfig"></a>NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG

微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_CONFIG 通知来告知在前一次完成移动宽带 (MB) 服务[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)查询或设置请求。

未经请求的事件会发送默认 LTE 附加如果上下文更新网络，通过无线 (OTA) 或短消息服务 (SMS)。 在这种情况下，微型端口驱动程序必须更新默认 LTE 附加上下文并将此通知发送到主机操作系统使用的更新列表。

此状态通知使用[ **NDIS_WWAN_LTE_ATTACH_CONTEXTS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1703 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>另请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_CONFIG](oid-wwan-lte-attach-config.md)

[**NDIS_WWAN_LTE_ATTACH_CONTEXTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_contexts)
