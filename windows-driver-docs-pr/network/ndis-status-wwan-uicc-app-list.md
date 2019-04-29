---
title: NDIS_STATUS_WWAN_UICC_APP_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_APP_LIST 通知来通知关于完成的上一个 OID_WWAN_UICC_APP_LIST 查询请求的移动宽带 (MB) 服务。
ms.assetid: D18BA7C8-5CEC-4DF6-BB5A-C8F65E1911A5
ms.date: 04/08/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_APP_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f3ea5ed361af7250f198306dee9d0a04bdd8b331
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384642"
---
# <a name="ndisstatuswwanuiccapplist"></a>NDIS_STATUS_WWAN_UICC_APP_LIST

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_APP_LIST**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)查询请求。

未经请求的事件不适用。

使用此通知[ **NDIS_WWAN_UICC_APP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)
