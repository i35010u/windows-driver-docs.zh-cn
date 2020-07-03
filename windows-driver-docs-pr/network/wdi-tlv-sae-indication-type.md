---
title: WDI_TLV_SAE_INDICATION_TYPE
description: WDI_TLV_SAE_INDICATION_TYPE 是一种 TLV，其中包含继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者表明身份验证无法继续的通知。
ms.assetid: F505CA27-4B2F-4210-8BE4-F3B931B86DDC
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_INDICATION_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c18e537352aa073fac0e705986bd360d584b2daf
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916776"
---
# <a name="wdi_tlv_sae_indication_type"></a>WDI_TLV_SAE_INDICATION_TYPE

**WDI_TLV_SAE_INDICATION_TYPE**是一种 TLV，其中包含继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者表明身份验证无法继续的通知。

此 TLV 在[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中使用。

## <a name="tlv-type"></a>TLV 类型

0x14B

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) | 继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者无法继续进行身份验证的通知。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
