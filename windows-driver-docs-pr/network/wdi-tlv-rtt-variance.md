---
title: WDI_TLV_RTT_VARIANCE
description: WDI_TLV_RTT_VARIANCE 是一种 TLV，其中包含当使用了多个度量值时，在精细计时度量（INTERNAL.H）请求期间用于计算往返时间（RTT）的度量值的统计方差。
ms.assetid: F8032726-4CC8-40F4-8FA1-840A3514A4B0
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT_VARIANCE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ae8edd015d9bb17ab8cdb2fe383569665ce9be5a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918227"
---
# <a name="wdi_tlv_rtt_variance"></a>WDI_TLV_RTT_VARIANCE

**WDI_TLV_RTT_VARIANCE**是一种 TLV，其中包含当使用了多个度量值时，在精细计时度量（internal.h）请求期间用于计算往返时间（RTT）的度量值的统计方差。 

此 TLV 用于[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15E

## <a name="length"></a>长度

UINT64 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| UINT64 | 用于计算 RTT 的度量值的统计方差。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
