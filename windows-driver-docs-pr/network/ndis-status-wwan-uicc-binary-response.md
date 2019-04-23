---
title: NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE 通知来通知关于完成的上一个 OID_WWAN_UICC_ACCESS_BINARY 查询请求的移动宽带 (MB) 服务。
ms.assetid: DA4EAA85-C24F-42FC-98D7-075F49A35672
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 64957bf1d68b0b4d61858537a1330cee5217e109
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905230"
---
# <a name="ndisstatuswwanuiccbinaryresponse"></a>NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)查询或设置请求。

未经请求的事件不适用。

使用此通知[ **NDIS_WWAN_UICC_RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10，版本 1903 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
