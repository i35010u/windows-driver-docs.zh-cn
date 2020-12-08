---
title: NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_MODEM_LOGGING_CONFIG 查询或设置请求的完成有关。
ms.date: 04/11/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b76c2902259a21a6e0b69cfc24de2d11c912fec1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822909"
---
# <a name="ndis_status_wwan_modem_logging_config"></a>NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG

微型端口驱动程序使用 **NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md) 查询或设置请求的完成有关。

小型端口驱动程序将此通知作为未经请求的事件发送，在这种情况下，调制解调器需要向操作系统通知内部更改。 目前，Windows 10 版本1903中不会出现这些情况。

此通知使用 [**NDIS_WWAN_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[使用 DSS 进行 MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
