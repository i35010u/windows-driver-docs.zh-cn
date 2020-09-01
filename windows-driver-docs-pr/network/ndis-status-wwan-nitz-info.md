---
title: NDIS_STATUS_WWAN_NITZ_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_NITZ_INFO 通知来通知移动宽带 (MB) 服务，以了解以前的 OID_WWAN_NITZ 查询请求是否完成。
ms.assetid: 8AC20FB1-FD2E-46B4-97F7-56EC7AA79740
ms.date: 04/11/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_NITZ_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0e3a382fa4447d99402fd8abca0ddd38e633e0bf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213423"
---
# <a name="ndis_status_wwan_nitz_info"></a>NDIS_STATUS_WWAN_NITZ_INFO

微型端口驱动程序使用 **NDIS_STATUS_WWAN_NITZ_INFO** 通知来通知移动宽带 (MB) 服务，以了解以前的 [OID_WWAN_NITZ](oid-wwan-nitz.md) 查询请求是否完成。

微型端口驱动程序以未经请求的事件的形式发送此通知，以提供当前网络时间和时区的 intformation。

此通知使用 [**NDIS_WWAN_NITZ_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[使用 DSS 进行 MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[OID_WWAN_NITZ](oid-wwan-nitz.md)

[**NDIS_WWAN_NITZ_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)