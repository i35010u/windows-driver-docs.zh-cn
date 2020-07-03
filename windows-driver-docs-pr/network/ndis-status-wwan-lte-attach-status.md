---
title: NDIS_STATUS_WWAN_LTE_ATTACH_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_LTE_ATTACH_STATUS 查询请求。
ms.assetid: 8A40437E-7AAC-4829-A032-0B8C933A7AC0
ms.date: 08/23/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8e6255dea6605710f1a2cd49637505dae6e1572f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916158"
---
# <a name="ndis_status_wwan_lte_attach_status"></a>NDIS_STATUS_WWAN_LTE_ATTACH_STATUS

微型端口驱动程序使用 NDIS_STATUS_WWAN_LTE_ATTACH_STATUS 通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)查询请求。

如果激活了用于 LTE 附加的上下文，则会发送未经请求的事件，例如插入 SIM 的时间。 在这种情况下，微型端口驱动程序应将此通知发送到主机操作系统。

此状态通知使用[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[OID_WWAN_LTE_ATTACH_STATUS](oid-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)
