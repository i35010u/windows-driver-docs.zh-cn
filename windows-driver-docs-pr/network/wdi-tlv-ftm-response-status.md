---
title: WDI_TLV_FTM_RESPONSE_STATUS
description: WDI_TLV_FTM_RESPONSE_STATUS 是一种 TLV，其中包含来自目标 BSS 的精细计时度量值（INTERNAL.H）响应状态。
ms.assetid: 49C3759C-3F3F-4C2D-863E-28227ED323BA
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_FTM_RESPONSE_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 64444f4a79a6aeef786346ac0aa838c4c7a39b86
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917343"
---
# <a name="wdi_tlv_ftm_response_status"></a>WDI_TLV_FTM_RESPONSE_STATUS

**WDI_TLV_FTM_RESPONSE_STATUS**是一种 TLV，其中包含来自目标 BSS 的精细计时度量值（internal.h）响应状态。

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x159

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ftm_response_status) | INTERNAL.H 响应状态。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
