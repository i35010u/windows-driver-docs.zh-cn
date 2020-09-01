---
title: OID_WWAN_MODEM_LOGGING_CONFIG
description: OID_WWAN_MODEM_LOGGING_CONFIG 用于配置调制解调器收集的日志以及在数据服务流 (DSS) 上将它们从调制解调器发送到主机的频率。
ms.assetid: 418157C2-27B4-4007-9FC4-BEEFEE8EB88B
ms.date: 04/11/2019
keywords:
- 从 Windows Vista 开始 OID_WWAN_MODEM_LOGGING_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: df09b6ffd9af6b7afae7686ecf441bf09f588f37
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216984"
---
# <a name="oid_wwan_modem_logging_config"></a>OID_WWAN_MODEM_LOGGING_CONFIG

OID_WWAN_MODEM_LOGGING_CONFIG 用于配置调制解调器收集的日志以及在数据服务流 (DSS) 上将它们从调制解调器发送到主机的频率。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送 [NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md) 状态通知，其中包含描述当前调制解调器日志记录配置的 [**NDIS_WWAN_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config) 结构。

设置负载包含指定如何配置调制解调器日志记录的 [**NDIS_WWAN_SET_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config) 结构。 微型端口驱动程序必须异步处理设置请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送 [NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md) 状态通知，其中包含在设置请求后描述调制解调器日志记录配置的 [**NDIS_WWAN_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config) 结构。

## <a name="remarks"></a>备注

在启动日志记录会话之前，必须配置日志记录。 这是一个可选 OID，用于支持的微型端口驱动程序。 但是，如果微型端口驱动程序支持通过 DSS 通道进行的调制解调器日志记录，则必须指定它支持此 OID。 

有关此 OID 的用法的详细信息，请参阅 [使用 DSS 进行 MB 的调制解调器日志记录](mb-modem-logging-with-dss.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[使用 DSS 进行 MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)

[**NDIS_WWAN_SET_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)