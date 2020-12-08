---
title: WDI_TLV_RTT_VARIANCE
description: WDI_TLV_RTT_VARIANCE 是一种 TLV，其中包含用于计算在精确计时)  (度量期间（如果使用了多个度量值） (RTT) 进行往返时间的度量值的统计方差。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT_VARIANCE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 048c1d00fd9d9385d71c602f31df6b4a0e9b8034
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834243"
---
# <a name="wdi_tlv_rtt_variance"></a>WDI_TLV_RTT_VARIANCE

**WDI_TLV_RTT_VARIANCE** 是一种 TLV，其中包含用于计算在精确计时)  (度量期间（如果使用了多个度量值） (RTT) 进行往返时间的度量值的统计方差。 

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15E

## <a name="length"></a>长度

UINT64) 大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT64 | 用于计算 RTT 的度量值的统计方差。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
