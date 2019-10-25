---
title: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
description: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
ms.assetid: 3BD36C57-BEE3-4BC8-BDF3-480E4066777A
ms.date: 02/14/2019
keywords:
- NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 784afe774ac10a3c9da8869d6e0769f68fa15bb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843396"
---
# <a name="ndis_status_wdi_indication_sae_auth_params_needed"></a>NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED

Wi-fi 适配器发送此指示来请求参数，以同时进行 Equals （SAE）身份验证。

当请求微型端口驱动程序以使用目标 BSSID 执行 SAE authentication 时，它需要在身份验证的各个阶段请求信息。 最初，它为提交请求帧请求参数，并在成功时请求确认请求帧。 如果驱动程序遇到无法恢复的超时或错误，还会指示到操作系统。

此指示在 SAE authentication 过程中发送。 有关详细信息，请参阅[WPA3-SAE authentication](wpa3-sae-authentication.md)。

## <a name="payload-data"></a>负载数据

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | AP 的 BSS ID。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) |   |   | 继续对 BSSID 进行 SAE 身份验证所需的信息的类型，或者无法继续进行身份验证的通知。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | TLV\<LIST\<UINT8 > > |   | X | SAE 提交响应帧。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | TLV\<LIST\<UINT8 > > |   | X | SAE 确认响应帧。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE authentication 失败错误状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Dot11wdi |
