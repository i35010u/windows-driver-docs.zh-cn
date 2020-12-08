---
title: OID_WWAN_UICC_ACCESS_BINARY
description: OID_WWAN_UICC_ACCESS_BINARY 访问 UICC 二进制文件，其结构类型为 WwanUiccFileStructureTransparent 或 WwanUiccFileStructureBerTLV。
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 OID_WWAN_UICC_ACCESS_BINARY 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b1c98d3f5b5ed0c6bb5d22152de9195ba0127d7e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812879"
---
# <a name="oid_wwan_uicc_access_binary"></a>OID_WWAN_UICC_ACCESS_BINARY

OID_WWAN_UICC_ACCESS_BINARY 访问 UICC 二进制文件，其结构类型为 **WwanUiccFileStructureTransparent** 或 **WwanUiccFileStructureBerTLV**。

查询请求读取二进制文件。 查询负载包含一个 [**NDIS_WWAN_UICC_ACCESS_BINARY**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_binary) 结构，它指定要读取的文件的相关信息。 微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送 [NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE](ndis-status-wwan-uicc-binary-response.md) 状态通知，其中包含描述 UICC 响应的 [**NDIS_WWAN_UICC_RESPONSE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) 结构。 

## <a name="remarks"></a>备注

有关此 OID 的用法的详细信息，请参阅 [MB UICC 应用程序和文件系统访问](mb-uicc-application-and-file-system-access.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE](ndis-status-wwan-uicc-binary-response.md)

[**NDIS_WWAN_UICC_ACCESS_BINARY**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_access_binary) 

[**NDIS_WWAN_UICC_RESPONSE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
