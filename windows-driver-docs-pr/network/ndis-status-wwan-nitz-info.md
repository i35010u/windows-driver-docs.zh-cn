---
title: NDIS_STATUS_WWAN_NITZ_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_NITZ_INFO 通知来通知移动宽带 (MB) 服务，以了解以前的 OID_WWAN_NITZ 查询请求是否完成。
ms.date: 04/11/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_NITZ_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0775dcd4c329543d4f02ca4addd8580394f88c8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820603"
---
# <a name="ndis_status_wwan_nitz_info"></a>NDIS_STATUS_WWAN_NITZ_INFO

微型端口驱动程序使用 **NDIS_STATUS_WWAN_NITZ_INFO** 通知来通知移动宽带 (MB) 服务，以了解以前的 [OID_WWAN_NITZ](oid-wwan-nitz.md) 查询请求是否完成。

微型端口驱动程序以未经请求的事件的形式发送此通知，以提供当前网络时间和时区的 intformation。

此通知使用 [**NDIS_WWAN_NITZ_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[使用 DSS 进行 MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[OID_WWAN_NITZ](oid-wwan-nitz.md)

[**NDIS_WWAN_NITZ_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)
