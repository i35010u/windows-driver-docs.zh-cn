---
title: OID_WWAN_UICC_FILE_STATUS
description: OID_WWAN_UICC_FILE_STATUS 检索有关指定 UICC 文件的信息。
ms.assetid: 1FD3E140-1CE3-416C-8CB4-27012363B60B
ms.date: 04/09/2019
keywords: -OID_WWAN_UICC_FILE_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 62c39aa0f07d354ea2bfec8e350dfb4568889ad8
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905277"
---
# <a name="oidwwanuiccfilestatus"></a>OID_WWAN_UICC_FILE_STATUS

OID_WWAN_UICC_FILE_STATUS 检索有关指定 UICC 文件的信息。 

查询有效负载包含[ **NDIS_WWAN_UICC_FILE_PATH** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_path)结构，它包含有关目标文件的信息。 微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_UICC_FILE_STATUS](ndis-status-wwan-uicc-file-status.md)状态通知包含[ **NDIS_WWAN_UICC_FILE_STATUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)结构，它描述指定的文件。 

不适用集发出的请求。

## <a name="remarks"></a>备注

有关此 OID 的使用情况的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_FILE_STATUS](ndis-status-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_PATH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_path) 

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
