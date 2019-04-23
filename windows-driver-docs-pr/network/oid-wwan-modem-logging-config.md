---
title: OID_WWAN_MODEM_LOGGING_CONFIG
description: OID_WWAN_MODEM_LOGGING_CONFIG 用于配置日志收集的调制解调器和何种频率它们将发送从调制解调器到主机对数据服务 Stream (DSS)。
ms.assetid: 418157C2-27B4-4007-9FC4-BEEFEE8EB88B
ms.date: 04/11/2019
keywords:
- 从 Windows Vista 开始 OID_WWAN_MODEM_LOGGING_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 57d5cb10e3ac4a8e393b5f69c7caeb308251fb9a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905263"
---
# <a name="oidwwanmodemloggingconfig"></a>OID_WWAN_MODEM_LOGGING_CONFIG

OID_WWAN_MODEM_LOGGING_CONFIG 用于配置日志收集的调制解调器和何种频率它们将发送从调制解调器到主机对数据服务 Stream (DSS)。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)状态通知包含[ **NDIS_WWAN_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)结构，描述当前调制解调器日志记录配置。

设置有效负载包含[ **NDIS_WWAN_SET_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)结构，它指定如何配置调制解调器日志记录。 微型端口驱动程序必须设置异步处理请求，最初在更高版本发送之前对原始请求返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)状态通知包含[ **NDIS_WWAN_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)结构描述后集请求的调制解调器日志记录配置。

## <a name="remarks"></a>备注

在启动日志记录会话之前，必须配置日志记录。 这是以支持微型端口驱动程序的可选 OID。 但是，如果微型端口驱动程序支持通过 DSS 通道的调制解调器日志记录，它必须指定它支持此 OID。 

有关此 OID 的使用情况的详细信息，请参阅[MB 的调制解调器日志记录与 DSS](mb-modem-logging-with-dss.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[使用 DSS MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG](ndis-status-wwan-modem-logging-config.md)

[**NDIS_WWAN_SET_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_modem_logging_config)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
