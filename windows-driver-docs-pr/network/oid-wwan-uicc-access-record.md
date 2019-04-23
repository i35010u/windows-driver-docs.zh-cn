---
title: OID_WWAN_UICC_ACCESS_RECORD
description: OID_WWAN_UICC_ACCESS_RECORD 访问 UICC 线性固定或循环文件，该结构类型是 WwanUiccFileStructureCyclic 或 WwanUiccFileStructureLinear。
ms.assetid: 450F397E-AC91-4239-BF60-B0DEB2F065DA
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 OID_WWAN_UICC_ACCESS_RECORD 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7e92bd5d5a8e5ffc5f3277b95e5acd31e16f0dca
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905232"
---
# <a name="oidwwanuiccaccessrecord"></a>OID_WWAN_UICC_ACCESS_RECORD

OID_WWAN_UICC_ACCESS_RECORD 访问 UICC 线性固定或循环文件，其中的结构类型是**WwanUiccFileStructureCyclic**或**WwanUiccFileStructureLinear**。

查询请求读取记录的内容。 查询有效负载包含[ **NDIS_WWAN_UICC_ACCESS_RECORD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)结构，它指定要读取的文件有关的信息。 微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)状态通知包含[ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)介绍 UICC 的响应的结构。 

设置请求更新的线性固定或循环文件。 设置有效负载包含[ **NDIS_WWAN_UICC_ACCESS_RECORD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)结构，它指定要向其写入文件的信息。 微型端口驱动程序必须设置异步处理请求，最初在更高版本发送之前对原始请求返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)状态通知包含[ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)介绍 UICC 的响应的结构。 

## <a name="remarks"></a>备注

有关此 OID 的使用情况的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)

[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
