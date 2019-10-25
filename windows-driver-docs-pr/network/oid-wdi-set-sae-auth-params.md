---
title: OID_WDI_SET_SAE_AUTH_PARAMS
description: OID_WDI_SET_SAE_AUTH_PARAMS 由 WDI 发送，以响应来自驱动程序的 NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED 指示。 它包含为 Equals （SAE） Commit 或 Confirm 请求同时发送身份验证所需的参数，或指示无法使用 BSSID 执行 SAE 的错误消息。
ms.assetid: D20F92F9-8AEF-456C-B27A-20E61F75B3B7
ms.date: 02/15/2019
keywords:
- OID_WDI_SET_SAE_AUTH_PARAMS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6e465d32aaaa9abc398752498193ec423dcdaf40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843872"
---
# <a name="oid_wdi_set_sae_auth_params"></a>OID_WDI_SET_SAE_AUTH_PARAMS

**OID_WDI_SET_SAE_AUTH_PARAMS**由 WDI 发送，以响应来自驱动程序的[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)指示。 它包含为 Equals （SAE） Commit 或 Confirm 请求同时发送身份验证所需的参数，或指示无法使用 BSSID 执行 SAE 的错误消息。 

此命令作为对驱动程序的直接 OID 请求发送。

有关 SAE authentication 的详细信息，请参阅[WPA3 SAE authentication](wpa3-sae-authentication.md)。

## <a name="command-parameters"></a>命令参数

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |  | AP 的 BSSID。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | [**WDI_SAE_REQUEST_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_request_type) |   |   | 要发送到 BSSID 的 SAE 请求帧的类型。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | WDI_SAE_COMMIT_REQUEST |  | X | SAE 提交请求参数。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | WDI_SAE_CONFIRM_REQUEST |  | X | SAE 确认请求参数。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE 身份验证失败错误状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Dot11wdi |
