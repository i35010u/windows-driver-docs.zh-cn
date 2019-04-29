---
title: 接收段合并的示例
description: 本部分使用的段按顺序接收和处理单个延缓的过程调用 (DPC) 中的示例演示了合并的算法。
ms.assetid: BC4C3216-683B-4E86-B2DF-F75FFCA7DACC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abf61775d1421eaf92e4d26954cc00786198881d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385495"
---
# <a name="examples-of-receive-segment-coalescing"></a>接收段合并的示例


本部分使用的段按顺序接收和处理单个延缓的过程调用 (DPC) 中的示例演示了合并的算法。

此页面只使用 X 和 X 进行标记后续段。 所有其他段和单个合并的单元 (SCU) 字段是如中所述[规则合并 TCP/IP 段](rules-for-coalescing-tcp-ip-packets.md)。

## <a name="example-1-data-segments"></a>示例 1：数据段


### <a name="segment-description"></a>段说明

属于同一个 TCP 连接的 10 个连续段进行处理。 所有以下条件，则为每个：

-   X’.SEQ == X.NXT

-   X’SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

没有任何这些段将生成异常。
### <a name="result"></a>结果

单个 SCU 超出 10 段构成。 这表示为单个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)在单个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388).

## <a name="example-2-data-segments-followed-by-an-exception-followed-by-data-segments"></a>示例 2：数据段后, 跟一个异常后, 跟数据段


### <a name="segment-description"></a>段说明

5 个连续细分属于同一个 TCP 连接进行处理。 所有以下条件，则为每个：

-   X’.SEQ == X.NXT

-   X’SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

没有任何这些段将生成异常。
第 6 段是一个重复的 ACK 段使用 SACK TCP 选项并生成基于规则号 3 中的异常[规则合并 TCP/IP 段](rules-for-coalescing-tcp-ip-packets.md)。

**请注意**  在这种情况下，用于处理 TCP 选项例外规则优先的因此重写合并规则。

 

处理 2 个连续的段属于同一个 TCP 连接。 所有以下条件，则为每个：

-   X’.SEQ == X.NXT

-   X’SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

没有任何这些段将生成异常。
### <a name="result"></a>结果

单个 SCU 超出前 5 个段构成。 第 6 段未形成 SCU。

第七个和第 8 个段一起构成 SCU。

一个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)具有三个指示链**NET\_缓冲区\_列表**结构每个拥有一个单独[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)。 接收的段的顺序进行维护。

## <a name="example-3-data-segments-followed-by-multiple-window-updates"></a>示例 3：数据段后, 跟多个窗口更新


### <a name="segment-description"></a>段说明

5 个连续细分属于同一个 TCP 连接进行处理。 所有以下条件，则为每个：

-   X’.SEQ == X.NXT

-   X’SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

没有任何这些段将生成异常。
第 6 段是 SEG 的窗口中更新了纯确认。WND = 65535，如下面的流程图中所示。

![描述规则使用 tcp 时间戳选项合并段的流程图](images/rsc-rules2.png)

第 7 个段是 SEG 的窗口中更新了纯确认。WND = 131070 相同流程图中所示。

### <a name="result"></a>结果

单个 SCU 超出 7 段构成。 这表示为单个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)在单个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388).

SCU。WND = 131070，并基于此值更新校验和。

## <a name="example-4-piggybacked-acks-mixed-with-data-segments"></a>示例 4：数据段的非法携带的确认混合


### <a name="segment-description"></a>段说明

3 个连续的段属于同一个 TCP 连接进行处理。 所有以下条件，则为每个：

-   X’.SEQ == X.NXT

-   X’SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

没有任何这些段将生成异常。
处理 2 个连续的段属于同一个 TCP 连接。 所有以下条件，则为每个：

-   X’.SEQ == X.NXT

-   X’SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

没有任何这些段将生成异常。
### <a name="result"></a>结果

单个 SCU 超出 5 段构成。 这表示为单个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)在单个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388). SCU。确认设置的最后一个 SEG.ACK。

 

 





