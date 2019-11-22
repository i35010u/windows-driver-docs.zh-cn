---
title: OID_WWAN_UICC_APP_LIST
description: OID_WWAN_UICC_APP_LIST 在 UICC 中检索应用程序的列表以及这些应用程序的相关信息。
ms.assetid: C2E8CDBC-453A-4697-9BD9-1197FBDA2455
ms.date: 04/08/2019
keywords: -从 Windows Vista 开始 OID_WWAN_UICC_APP_LIST 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 47eac27b7135245e64775ff89ab1a4054441ee72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843772"
---
# <a name="oid_wwan_uicc_app_list"></a>OID_WWAN_UICC_APP_LIST

OID_WWAN_UICC_APP_LIST 在 UICC 中检索应用程序的列表以及这些应用程序的相关信息。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)状态通知，其中包含描述 UICC 的应用列表的[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)结构。

设置请求不适用。

## <a name="remarks"></a>备注

当调制解调器中的 UICC 完全初始化并准备向移动运营商注册时，必须选择一个 UICC 应用程序进行注册，并且具有此 OID 的查询请求应在响应中使用的[**WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_app_list)结构的**ActiveAppIndex**字段中返回所选应用程序。

有关此 OID 的用法的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1903 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)

[**WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_app_list)
