---
title: WDI_TLV_RTT_ACCURACY
description: WDI_TLV_RTT_ACCURACY 是程度的包含的准确性或预期为好计时度量 (FTM) 请求的则返回 true 值的往返时间 (RTT) 度量程度 TLV。
ms.assetid: 689C9C22-6AA4-4581-BF26-147F49F2456F
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_RTT_ACCURACY 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a765cae38c9c1f153d5dcd54e94c176e7470dd45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359097"
---
# <a name="wditlvrttaccuracy"></a>WDI_TLV_RTT_ACCURACY

**WDI_TLV_RTT_ACCURACY**是包含的准确性或预期的程度为好计时度量 (FTM) 请求的则返回 true 值的往返时间 (RTT) 度量程度 TLV。 单位为 picoseconds 中。

例如，如果当前的 RTT 为 66712.82 picoseconds （从目标 AP 10 米），但它是已知通过硬件事件探查的测量值可能是关闭快/慢 1 米，则 RTT 准确性是 6671.28 picoseconds。 它负责 IHV 提供作为特定拍摄实际 FTM 时其硬件和匹配条件的分析基于尽可能精确。 有多个变量影响 FTM 准确性，可以测量和被视为多个可能性的这些变量。 更具体的准确性是理想的原因是因为这是可以使用较高的层，例如首选具有较高准确度计算位置时，或改变基于 FTM 准确性计算的位置错误度量的有用信息。 在分析时，应使用 CDF 最低 90%。 

在中使用此 TLV [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15D

## <a name="length"></a>长度

UINT32 大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| UINT32 | RTT。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
