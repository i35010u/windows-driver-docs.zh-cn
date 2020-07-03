---
title: NDIS_STATUS_WWAN_UICC_FILE_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_FILE_STATUS 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_UICC_FILE_STATUS 查询请求。
ms.assetid: ABC19EDC-E414-4783-BC3B-ECABDF06C0C5
ms.date: 04/09/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_FILE_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 09e6c1e4a2ad0e6c43ee8a2e121f9a685eab36d5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916632"
---
# <a name="ndis_status_wwan_uicc_file_status"></a>NDIS_STATUS_WWAN_UICC_FILE_STATUS

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_FILE_STATUS**通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)查询请求。

未经请求的事件不适用。

此通知使用[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
