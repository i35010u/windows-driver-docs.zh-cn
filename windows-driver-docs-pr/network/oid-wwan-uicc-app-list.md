---
title: OID_WWAN_UICC_APP_LIST
description: OID_WWAN_UICC_APP_LIST 检索 UICC 中的应用程序和其相关信息的列表。
ms.assetid: C2E8CDBC-453A-4697-9BD9-1197FBDA2455
ms.date: 04/08/2019
keywords: -从 Windows Vista 开始 OID_WWAN_UICC_APP_LIST 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1661b5eb4baf57a302e1e12b96c74fb9e4f88b47
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905343"
---
# <a name="oidwwanuiccapplist"></a>OID_WWAN_UICC_APP_LIST

OID_WWAN_UICC_APP_LIST 检索 UICC 中的应用程序和其相关信息的列表。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)状态通知包含[ **NDIS_WWAN_UICC_APP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)结构描述 UICC 应用列表。

不适用集发出的请求。

## <a name="remarks"></a>备注

当在调制解调器 UICC 完全初始化和准备好注册到移动运营商，UICC 应用程序必须选择用于注册和此 OID 的查询请求应返回所选应用程序中的**ActiveAppIndex**字段[ **WWAN_UICC_APP_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_uicc_app_list)响应中使用的结构。

有关此 OID 的使用情况的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_APP_LIST](ndis-status-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)

[**WWAN_UICC_APP_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_uicc_app_list)
