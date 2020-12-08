---
title: WDI_TLV_RTT_ACCURACY
description: WDI_TLV_RTT_ACCURACY 是一种 TLV，其中包含往返时间 (RTT 的准确性或预期度，RTT) 度量值设置为精细计时度量值 (INTERNAL.H) 请求。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT_ACCURACY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 40aaa19a7b08121e7832df7df52ba34af4118af3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818015"
---
# <a name="wdi_tlv_rtt_accuracy"></a>WDI_TLV_RTT_ACCURACY

**WDI_TLV_RTT_ACCURACY** 是一种 TLV，其中包含往返时间 (RTT 的准确性或预期度，RTT) 度量值设置为精细计时度量值 (internal.h) 请求。 单元位于 picoseconds 中。

例如，如果当前 RTT 为 66712.82 picoseconds 从目标 AP)  (10 米，但通过硬件分析知道测量可能会由 +/-1 米关闭，则 RTT 准确度为 6671.28 picoseconds。 IHV 的责任是根据其硬件分析和执行实际 INTERNAL.H 时的匹配条件，提供尽可能具体的准确性。 存在多个影响 INTERNAL.H 准确性的变量，以及可以对这些变量进行度量和考虑的多种可能性。 需要更具体的准确性的原因是，这是上层可以使用的有用信息，例如，在计算位置时使用更高准确性的首选度量值，或者根据 INTERNAL.H 准确性改变计算位置错误。 在分析时，应使用至少90% 的 CDF。 

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15D

## <a name="length"></a>长度

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
