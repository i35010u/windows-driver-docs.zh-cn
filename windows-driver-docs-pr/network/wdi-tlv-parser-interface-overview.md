---
title: WDI TLV 分析器接口概述
description: 本部分介绍 WDI TLV 分析程序接口的概述
ms.assetid: FD204F24-0336-4A54-992C-ACF46565D8D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b09a90c159a7260b4e29c86f83b4d2976d9ddd1f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210039"
---
# <a name="wdi-tlv-parser-interface-overview"></a>WDI TLV 分析器接口概述


## <a name="callee-allocation-model"></a>被调用方分配模型


驱动程序中的入口点接收包含 TLVs 的消息或指示。 在代码提取消息 ID 并确定它是否是它想要处理的 ID 后，它将调用一般分析例程并在 [**WDI \_ 消息 \_ 标头**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header) 前进后传递 TLV Blob () 将 TLVs 解析为 C 结构。

```c
ndisStatus = Parse(
    cbBufferLength,
    pvBuffer,
    messageId,
    &Context,
    &pParsed);
```

检查返回的错误后，代码可以将输出缓冲区 (*pParsed*) 转换为具体类型，如下面的示例中所示。

```c
((WDI_INDICATION_BSS_ENTRY_LIST_PARAMETERS*)pParsed)
```

调用方完成已分析的数据后，调用方必须将内存返回到分析器。 分析器需要知道用于分配的原始消息 ID，以便释放正确的数据。

```c
FreeParsed(messageId, pParsed);
pParsed = NULL;
```

## <a name="caller-allocation-model"></a>调用方分配模型


在此模型中，调用方已确定要分析的正确特定 TLV，并可能使用堆栈本地来避免在堆上分配。 调用方创建本地并调用特定的分析例程。 API 不需要消息 ID，并且参数为强类型，并且具有较低的间接级别。

```c
WDI_GET_ADAPTER_CAPABILITIES_PARAMETERS adapterCapabilitiesParsed;

ndisStatus = ParseWdiGetAdapterCapabilities(
    cbBufferLength,
    pvBuffer,
    &Context
    &adapterCapabilitiesParsed);
```

在调用方完成使用结构后，调用方应为分析器有机会清除它在分析过程中所做的任何分配，并擦除结构，以便可以重复使用它。 参数为强类型，因此调用方不需要任何其他参数。

```c
CleanupParsedWdiGetAdapterCapabilities(&adapterCapabilitiesParsed);
```

调用 CleanupParse API 后，结构中的所有数据都无效。

某些消息没有任何关联的数据。 为实现 API 的完整性，提供了适当命名的分析方法。 这些方法验证字节流是否为空。 为参数类型提供了 typedef，但如果使用调用方分配模型，则调用方也可以为 out 参数传递 NULL。 在所有情况下，分析器都通过返回常量空 parse 结构来避免任何分配。 调用方决不应向此返回空结构 (因此，唯一字段将命名为** \_ Reserved**) 。 这些消息记录为 "无附加数据"。 标头中的数据足够 "。

## <a name="message-direction"></a>消息方向


大多数消息的 M1 与 M0、M3 或 M4 的格式不同。 为满足此类消息，此类消息具有不同的分析和生成 Api。 对于 M1 消息，Api 遵循 Parse<em> &lt; MessageName &gt; </em>ToIhv 的命名约定，或生成<em> &lt; MessageName &gt; </em>ToIhv。 对于 M0、M3 或 M4 消息，Api 遵循 Parse<em> &lt; MessageName &gt; </em>FromIhv 的命名约定，或生成<em> &lt; MessageName &gt; </em>FromIhv。 但是，为了简化 IHV 小型端口中的代码，定义添加到别名分析<em> &lt; MessageName &gt; </em>以分析<em> &lt; MessageName &gt; </em>ToIhv 并生成<em> &lt; MessageName &gt; </em>以生成<em> &lt; MessageName &gt; </em>FromIhv。 如果需要分析自己的 M3 或生成 M1，则 IHV 代码只需要知道此别名。

## <a name="error-codes"></a>错误代码


TLV 分析器生成器可以返回多个不同 \_ 的 NDIS 状态代码。 有关详细信息，请查看 WPP 跟踪日志。 日志应始终指示根本原因。 下面是最常见的错误代码及其含义的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>在分析时，这表示固定大小的 TLV 的大小不正确。 对于列表，这意味着总体大小不是单个元素大小的偶数倍，或者元素比应有的元素多。 如果需要1个或多个元素，这也可能表示包含0个元素的列表。 如果需要0个元素，则 <em>Optional_IsPresent</em> 应设置为 FALSE (TLV 标头不应在字节流) 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_BUFFER_OVERFLOW</p></td>
<td align="left"><p>生成时，这表示由于数组中的元素数 (列表) ，它将溢出 TLV 标头中的2字节 <strong>长度</strong> 字段。 应减小元素数。 当外部 TLV (太多或太大而) 内部 TLVs 时，也会发生这种情况，并再次溢出标头的2字节 <strong>长度</strong> 字段。</p>
<p>在分析时，这表示某个 TLV 标头的 <strong>长度</strong> 字段大于外部 TLV 或字节流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_FILE_NOT_FOUND</p></td>
<td align="left"><p>在分析时，这表示字节流中不存在所需的 TLV。 它通常是包含字节流的生成器的 bug。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_RESOURCES</p></td>
<td align="left"><p>生成时，这表示分配器失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_UNSUPPORTED_REVISION</p></td>
<td align="left"><p>分析或生成时， <strong>上下文</strong> 参数为 NULL，或 <strong>PeerVersion</strong> 小于 <strong>WDI_VERSION_MIN_SUPPORTED</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

