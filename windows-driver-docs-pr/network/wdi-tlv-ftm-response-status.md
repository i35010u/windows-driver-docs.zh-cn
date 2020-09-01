---
title: WDI_TLV_FTM_RESPONSE_STATUS
description: WDI_TLV_FTM_RESPONSE_STATUS 是一种 TLV，其中包含从目标 BSS (INTERNAL.H) 响应状态的精细计时度量值。
ms.assetid: 49C3759C-3F3F-4C2D-863E-28227ED323BA
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_RESPONSE_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 45b8e72c51e3b4f1c79a9b3ad49e9dce723db01d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209613"
---
# <a name="wdi_tlv_ftm_response_status"></a>WDI_TLV_FTM_RESPONSE_STATUS

**WDI_TLV_FTM_RESPONSE_STATUS** 是一种 TLV，其中包含从目标 BSS (internal.h) 响应状态的精细计时度量值。

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x159

## <a name="length"></a>Length

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| [**WDI_FTM_RESPONSE_STATUS**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ftm_response_status) | INTERNAL.H 响应状态。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp