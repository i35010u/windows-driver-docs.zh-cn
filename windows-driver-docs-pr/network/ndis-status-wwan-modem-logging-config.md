---
title: NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 通知来通知关于完成的上一个 OID_WWAN_MODEM_LOGGING_CONFIG 查询或一组请求的移动宽带 (MB) 服务。
ms.assetid: 0370C672-B7A7-4ECE-94F6-FC04407959E4
ms.date: 04/11/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d20ccc643575337460d0fb88ca713be132c8ad47
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905260"
---
# <a name="ndisstatuswwanmodemloggingconfig"></a>NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG

微型端口驱动程序使用**NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)查询或设置请求。

微型端口驱动程序发送此通知作为方案中的未经请求事件调制解调器需要操作系统情况通知给内部更改。 目前，在 Windows 10，版本 1903，这些方案不会发生。

使用此通知[ **NDIS_WWAN_MODEM_LOGGING_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[使用 DSS MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
