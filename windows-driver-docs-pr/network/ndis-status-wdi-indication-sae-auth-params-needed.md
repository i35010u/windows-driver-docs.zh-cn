---
title: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
description: NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED
ms.assetid: 3BD36C57-BEE3-4BC8-BDF3-480E4066777A
ms.date: 02/14/2019
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 76caa33f1e808bc802446488fcffb4ba994a1a96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361047"
---
# <a name="ndisstatuswdiindicationsaeauthparamsneeded"></a>NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED

Wi-fi 适配器将这种指示发送到同时进行身份验证的等于 (SAE) 身份验证的请求参数。

当请求微型端口驱动程序来执行与目标 BSSID SAE 身份验证时，它需要请求身份验证的各个阶段的信息。 最初，它将请求提交请求帧，然后在确认请求帧如果成功，则参数。 如果该驱动程序遇到不可恢复的超时或错误时，它还指示的操作系统。

此指示发送 SAE 身份验证过程。 有关详细信息，请参阅[WPA3 SAE 身份验证](wpa3-sae-authentication.md)。

## <a name="payload-data"></a>有效负载数据

| TLV | 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | AP BSS ID。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_indication_type) |   |   | 继续使用 bssid 时或通知 SAE 身份验证所需的信息类型的身份验证无法继续。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | TLV\<LIST\<UINT8>> |   | X | SAE 提交响应帧中。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | TLV\<LIST\<UINT8>> |   | X | SAE 确认响应帧中。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_sae_status) |   | X | SAE 身份验证失败错误状态。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |
