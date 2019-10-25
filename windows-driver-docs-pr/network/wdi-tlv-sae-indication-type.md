---
title: WDI_TLV_SAE_INDICATION_TYPE
description: WDI_TLV_SAE_INDICATION_TYPE 是一个 TLV，其中包含使用目标 BSSID 继续 SAE 身份验证所需的信息的类型，或者表明身份验证无法继续的通知。
ms.assetid: F505CA27-4B2F-4210-8BE4-F3B931B86DDC
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_INDICATION_TYPE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 62c64663611e2f77b9ddb5955b1351d96d3938ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841742"
---
# <a name="wdi_tlv_sae_indication_type"></a>WDI_TLV_SAE_INDICATION_TYPE

**WDI_TLV_SAE_INDICATION_TYPE**是一个 TLV，其中包含使用目标 BSSID 继续 SAE 身份验证所需的信息的类型，或者表明身份验证无法继续的通知。

此 TLV 在[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中使用。

## <a name="tlv-type"></a>TLV 类型

0x14B

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_SAE_INDICATION_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_indication_type) | 继续使用目标 BSSID 进行 SAE 身份验证所需的信息的类型，或者无法继续进行身份验证的通知。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
