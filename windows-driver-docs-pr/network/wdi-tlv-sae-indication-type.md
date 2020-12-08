---
title: WDI_TLV_SAE_INDICATION_TYPE
description: WDI_TLV_SAE_INDICATION_TYPE 是一种 TLV，其中包含继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者表明身份验证无法继续的通知。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_INDICATION_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 10f7946bc49530b078d9612778058522f29b09d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834209"
---
# <a name="wdi_tlv_sae_indication_type"></a>WDI_TLV_SAE_INDICATION_TYPE

**WDI_TLV_SAE_INDICATION_TYPE** 是一种 TLV，其中包含继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者表明身份验证无法继续的通知。

此 TLV 在 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中使用。

## <a name="tlv-type"></a>TLV 类型

0x14B

## <a name="length"></a>长度

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| [**WDI_SAE_INDICATION_TYPE**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) | 继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者无法继续进行身份验证的通知。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
