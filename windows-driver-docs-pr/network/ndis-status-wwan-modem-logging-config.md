---
title: NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_MODEM_LOGGING_CONFIG 查询或设置请求。
ms.assetid: 0370C672-B7A7-4ECE-94F6-FC04407959E4
ms.date: 04/11/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 20c4c129c40b7696e7df4e3d53435e3a8c52c281
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843276"
---
# <a name="ndis_status_wwan_modem_logging_config"></a>NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG

微型端口驱动程序使用**NDIS_STATUS_WWAN_MODEM_LOGGING_CONFIG**通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)查询或设置请求。

小型端口驱动程序将此通知作为未经请求的事件发送，在这种情况下，调制解调器需要向操作系统通知内部更改。 目前，Windows 10 版本1903中不会出现这些情况。

此通知使用[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1903 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[MB 的调制解调器日志记录](mb-modem-logging-with-dss.md)

[OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

[**NDIS_WWAN_MODEM_LOGGING_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_modem_logging_config)
