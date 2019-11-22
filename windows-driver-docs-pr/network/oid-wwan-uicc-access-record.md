---
title: OID_WWAN_UICC_ACCESS_RECORD
description: OID_WWAN_UICC_ACCESS_RECORD 访问 UICC 线性固定或循环文件，其结构类型为 WwanUiccFileStructureCyclic 或 WwanUiccFileStructureLinear。
ms.assetid: 450F397E-AC91-4239-BF60-B0DEB2F065DA
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 OID_WWAN_UICC_ACCESS_RECORD 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 283f8ea15e012d62a531ac73501a5c5225c7c3e4
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443009"
---
# <a name="oid_wwan_uicc_access_record"></a>OID_WWAN_UICC_ACCESS_RECORD

OID_WWAN_UICC_ACCESS_RECORD 访问 UICC 线性固定或循环文件，其结构类型为**WwanUiccFileStructureCyclic**或**WwanUiccFileStructureLinear**。

查询请求读取记录的内容。 查询负载包含一个[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)结构，它指定要读取的文件的相关信息。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)状态通知，其中包含描述 UICC 响应的[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)结构。 

## <a name="remarks"></a>备注

有关此 OID 的用法的详细信息，请参阅[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 版本 | Windows 10 版本 1903 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE](ndis-status-wwan-uicc-record-response.md)

[**NDIS_WWAN_UICC_ACCESS_RECORD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_record)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
