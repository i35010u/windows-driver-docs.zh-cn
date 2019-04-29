---
title: WDI TLV 分析器接口概述
description: 本部分介绍 WDI TLV 分析器界面的概述
ms.assetid: FD204F24-0336-4A54-992C-ACF46565D8D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dbc589320da8a58a13eea02299398db9e8b2f28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377878"
---
# <a name="wdi-tlv-parser-interface-overview"></a>WDI TLV 分析器接口概述


## <a name="callee-allocation-model"></a>被调用方分配模型


在驱动程序中的入口点接收消息或包含 TLVs 的指示。 在代码中提取的消息 ID 和确定它是否想要处理的 ID，它调用的泛型的分析例程，并通过 TLV blob 后 (后过去的提前[ **WDI\_消息\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn926074)) 将解析为 C 结构 TLVs。

```c
ndisStatus = Parse(
    cbBufferLength,
    pvBuffer,
    messageId,
    &Context,
    &pParsed);
```

检查是否有错误返回之后, 代码可以强制转换的输出缓冲区 (*pParsed*) 到具体类型，如在下面的示例。

```c
((WDI_INDICATION_BSS_ENTRY_LIST_PARAMETERS*)pParsed)
```

调用方完成的已分析数据之后，调用方必须返回内存分析器。 分析程序需要知道原始消息 ID 用于分配使它释放正确的数据。

```c
FreeParsed(messageId, pParsed);
pParsed = NULL;
```

## <a name="caller-allocation-model"></a>调用方分配模型


在此模型中，调用方已确定正确的特定 TLV 分析，并可能使用本地堆栈以避免在堆上的分配。 调用方创建本地，并调用特定的分析例程。 该 API 不需要的消息 ID，并使用一个更少级别的间接寻址强类型参数。

```c
WDI_GET_ADAPTER_CAPABILITIES_PARAMETERS adapterCapabilitiesParsed;

ndisStatus = ParseWdiGetAdapterCapabilities(
    cbBufferLength,
    pvBuffer,
    &Context
    &adapterCapabilitiesParsed);
```

调用方完成使用的结构之后，调用方应为分析器提供机会清理分析过程中，所做的任何分配并擦除结构，因此它已准备好可重复使用。 强类型参数，因此被调用方不需要任何其他参数。

```c
CleanupParsedWdiGetAdapterCapabilities(&adapterCapabilitiesParsed);
```

在调用之后 CleanupParse API，该结构中的所有数据都是无效的。

某些消息不具有任何关联的数据。 为了保持完整性的 api，提供适当命名的分析方法。 这些方法验证字节流为空。 Typedef 提供的参数类型，但调用方还可以传递 NULL 输出参数为如果它们使用调用方分配模型。 在所有情况下，分析器可以通过返回一个常量空分析结构避免任何分配。 调用方应永远不会写入此返回的空结构 (因此名为唯一字段**\_保留**)。 这些消息被记录为"没有其他数据。 标头中的数据就足够了"。

## <a name="message-direction"></a>消息传送方向


大多数消息都具有不同的格式为，而其 M0、 M3 或 M4 其 M1。 为了适应这，此类消息具有不同的分析和生成 Api。 M1 消息 Api 遵循分析的命名约定<em>&lt;MessageName&gt;</em>ToIhv 或生成<em>&lt;MessageName&gt;</em>ToIhv。 M0、 M3 或 M4 消息 Api 遵循分析的命名约定<em>&lt;MessageName&gt;</em>FromIhv 或生成<em>&lt;MessageName&gt;</em> FromIhv。 但是，为了简化 IHV 微型端口中的代码定义添加到别名 Parse<em>&lt;MessageName&gt;</em> 为 Parse<em>&lt;MessageName&gt;</em>ToIhv 和生成<em>&lt;MessageName&gt;</em> 生成<em>&lt;MessageName&gt;</em>FromIhv。 IHV 代码只需需要注意的此别名，如果需要分析其自己 M3，或生成 M1。

## <a name="error-codes"></a>错误代码


TLV 分析器生成器可以返回多个不同的 NDIS\_状态代码。 有关详细信息，查看 WPP 跟踪日志。 日志应始终指示根本原因。 下面是最常见的错误代码及其含义的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>在分析时，这指示固定大小的 TLV 是大小不正确。 有关列表，这意味着总体大小不是单个元素大小的偶数倍，或有更多元素不应进行。 这可能意味着需要 1 个或多时，列表包含 0 个元素。 如果需要 0 个元素，然后<em>Optional_IsPresent</em>应设置为 false （TLV 标头不应在字节流中）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_BUFFER_OVERFLOW</p></td>
<td align="left"><p>当生成时，这表示，由于数组 （列表） 中的元素数量，因此它溢出 2 个字节<strong>长度</strong>内 TLV 标头字段。 您应减少元素的数。 当外部 TLV 具有太多 （或太大的） 内部 TLVs，再次溢出 2 字节这也会发生<strong>长度</strong>标头的字段。</p>
<p>在分析时，这表示 TLV 标头<strong>长度</strong>字段大于外部 TLV 或字节流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_FILE_NOT_FOUND</p></td>
<td align="left"><p>在分析时，这表示需要的 TLV 不存在字节流中。 它通常是使用字节流的生成器的 bug。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_RESOURCES</p></td>
<td align="left"><p>当生成时，这表示分配器失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_UNSUPPORTED_REVISION</p></td>
<td align="left"><p>当分析或生成，<strong>上下文</strong>参数为 NULL，或<strong>PeerVersion</strong>是小于<strong>WDI_VERSION_MIN_SUPPORTED</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 





