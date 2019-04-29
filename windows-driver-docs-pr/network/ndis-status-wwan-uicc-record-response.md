---
title: NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 通知来通知关于完成的上一个 OID_WWAN_UICC_ACCESS_RECORD 查询请求的移动宽带 (MB) 服务。
ms.assetid: 5F729855-1056-43D3-BEF8-A2A2D4CA56CB
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3154bb247695748503a912aea42cc8d66ace21ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384635"
---
# <a name="ndisstatuswwanuiccrecordresponse"></a>NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)查询或设置请求。

未经请求的事件不适用。

使用此通知[ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
