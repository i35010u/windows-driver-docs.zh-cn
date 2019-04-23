---
title: NDIS_STATUS_WWAN_UICC_FILE_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_FILE_STATUS 通知来通知关于完成的上一个 OID_WWAN_UICC_FILE_STATUS 查询请求的移动宽带 (MB) 服务。
ms.assetid: ABC19EDC-E414-4783-BC3B-ECABDF06C0C5
ms.date: 04/09/2019
keywords: -NDIS_STATUS_WWAN_UICC_FILE_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3d5044299d100217d61e26fa8a96e8510a3100e9
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905265"
---
# <a name="ndisstatuswwanuiccfilestatus"></a>NDIS_STATUS_WWAN_UICC_FILE_STATUS

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_FILE_STATUS**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)查询请求.

未经请求的事件不适用。

使用此通知[ **NDIS_WWAN_UICC_FILE_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
