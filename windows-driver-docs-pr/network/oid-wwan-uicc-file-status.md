---
title: OID_WWAN_UICC_FILE_STATUS
description: OID_WWAN_UICC_FILE_STATUS 检索有关指定 UICC 文件的信息。
ms.assetid: 1FD3E140-1CE3-416C-8CB4-27012363B60B
ms.date: 04/09/2019
keywords: -从 Windows Vista 开始 OID_WWAN_UICC_FILE_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2e31b0892ca40b93738a35500f9aac423e25533f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917657"
---
# <a name="oid_wwan_uicc_file_status"></a>OID_WWAN_UICC_FILE_STATUS

OID_WWAN_UICC_FILE_STATUS 检索有关指定 UICC 文件的信息。 

查询负载包含包含目标文件相关信息的[**NDIS_WWAN_UICC_FILE_PATH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_path)结构。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送[NDIS_STATUS_WWAN_UICC_FILE_STATUS](ndis-status-wwan-uicc-file-status.md)状态通知，其中包含描述指定文件的[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)结构。 

设置请求不适用。

## <a name="remarks"></a>备注

有关此 OID 的用法的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_FILE_STATUS](ndis-status-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_PATH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_path) 

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
