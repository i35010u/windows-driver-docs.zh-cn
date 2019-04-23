---
title: NDIS_STATUS_WWAN_NITZ_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_NITZ_INFO 通知来通知关于完成的上一个 OID_WWAN_NITZ 查询请求的移动宽带 (MB) 服务。
ms.assetid: 8AC20FB1-FD2E-46B4-97F7-56EC7AA79740
ms.date: 04/11/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_NITZ_INFO 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 57b7e0c8bb8841e0ac9b889f223c3c2bc6020dbb
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905329"
---
# <a name="ndisstatuswwannitzinfo"></a>NDIS_STATUS_WWAN_NITZ_INFO

微型端口驱动程序使用**NDIS_STATUS_WWAN_NITZ_INFO**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_NITZ](oid-wwan-nitz.md)查询请求。

微型端口驱动程序将作为一个未经请求的事件，它提供当前的网络时间和时区 intformation 发送此通知。

使用此通知[ **NDIS_WWAN_NITZ_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[使用 DSS MB 调制解调器日志记录](mb-modem-logging-with-dss.md)

[OID_WWAN_NITZ](oid-wwan-nitz.md)

[**NDIS_WWAN_NITZ_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_nitz_info) 
