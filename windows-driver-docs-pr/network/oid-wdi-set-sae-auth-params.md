---
title: OID_WDI_SET_SAE_AUTH_PARAMS
description: WDI 发送 OID_WDI_SET_SAE_AUTH_PARAMS NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED 指示响应来自该驱动程序。 它包含发送同时进行身份验证的等于 (SAE) 提交或确认请求或指示执行与 BSSID SAE 失败的错误消息所必需的参数。
ms.assetid: D20F92F9-8AEF-456C-B27A-20E61F75B3B7
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_SAE_AUTH_PARAMS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 090fb0fe3d97293f250989526f608dbd19d0747e
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905334"
---
# <a name="oidwdisetsaeauthparams"></a>OID_WDI_SET_SAE_AUTH_PARAMS

**OID_WDI_SET_SAE_AUTH_PARAMS**在响应中发送的 WDI [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)驱动程序中的指示。 它包含发送同时进行身份验证的等于 (SAE) 提交或确认请求或指示执行与 BSSID SAE 失败的错误消息所必需的参数。 

此命令是作为直接 OID 请求发送到该驱动程序。

有关 SAE 身份验证的详细信息，请参阅[WPA3 SAE 身份验证](wpa3-sae-authentication.md)。

## <a name="command-parameters"></a>命令参数

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |  | AP BSSID。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_request_type) |   |   | SAE 请求帧为 bssid 时发送的类型。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | WDI_SAE_COMMIT_REQUEST |  | X | SAE 提交请求参数。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | WDI_SAE_CONFIRM_REQUEST |  | X | SAE 确认请求参数。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE 身份验证失败错误状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |
