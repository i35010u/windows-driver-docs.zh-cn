---
title: 故障分析项
description: DebugFailureAnalysis 对象具有失败分析条目的集合。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b87a01c4d49daff9981a95c6dcd8315056a72370
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826417"
---
# <a name="failure-analysis-entries"></a>故障分析项


[**DebugFailureAnalysis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有失败分析条目的集合。 有关详细信息，请参阅[故障分析条目、标记和数据类型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)。

*失败分析条目*（也称为*FA 条目*）是下列其中一项：

-   [**FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)结构
-   一个[**FA\_进入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)结构后跟一个数据块

[**FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)结构的**DataSize**成员保存数据块的大小（以字节为单位）。 如果没有数据块，则**DataSize**等于0。 **Fa\_条目**结构的**标记**成员标识存储在 FA 条目中的信息类型。 例如，标记**DEBUG\_FLR\_检测错误\_代码**指示**FA\_项**的数据块包含 bug 检查代码。

在某些情况下，不需要数据块;所有信息都由标记传达。 例如，具有标记**DEBUG\_FLR\_内核\_验证程序\_** 的[**FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)没有数据块。

每个标记都与 FA 中的一种数据类型相关联[ **\_条目\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ne-extsfns-_fa_entry_type)枚举。 例如，标记**debug\_FLR\_检测错误\_代码**与数据类型**调试\_FA\_ENTRY\_ULONG**相关联。 若要确定标记的数据类型，请调用[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)接口的[**GetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nf-extsfns-idebugfaentrytags-gettype)方法。

若要获取或设置 FA 条目的数据块，请使用[**IDebugFailureAnalysis2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)接口。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[正在写入分析扩展插件！分析](writing-an-analysis-extension-to-extend--analyze.md)

[**FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)

 

 






