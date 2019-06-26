---
title: 故障分析项
description: DebugFailureAnalysis 对象具有故障分析项的集合。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976d5ce21c7ce92c7e452974669bb5d45422ae39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366832"
---
# <a name="failure-analysis-entries"></a>故障分析项


一个[ **DebugFailureAnalysis** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有故障分析项的集合。 有关详细信息，请参阅[失败分析条目、 标记和数据类型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)。

一个*无法分析项*(也称为*FA 条目*) 是以下之一：

-   [ **FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)结构
-   [ **FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)结构后, 跟一个数据块

**DataSize**的成员[ **FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)结构保留大小，以字节为单位的数据块。 如果没有数据块， **DataSize**等于 0。 **标记**的成员**FA\_条目**结构标识的 FA 项中存储的信息种类。 例如，标记**调试\_FLR\_检测错误\_代码**指示数据块的**FA\_条目**包含错误检查代码。

在某些情况下，没有必要的数据块的;由标记传达的信息。 例如， [ **FA\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)标记**调试\_FLR\_内核\_VERIFIER\_已启用**不有任何数据块。

每个标记是与一个中的数据类型相关联[ **FA\_条目\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ne-extsfns-_fa_entry_type)枚举。 例如，标记**调试\_FLR\_检测错误\_代码**的数据类型与关联**调试\_FA\_条目\_ULONG**. 若要确定标记的数据类型，请调用[ **GetType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nf-extsfns-idebugfaentrytags-gettype)方法[IDebugFAEntryTags](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfaentrytags)接口。

若要获取或设置一个 FA 条目的数据块，使用[ **IDebugFailureAnalysis2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/nn-extsfns-idebugfailureanalysis2)接口。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[分析扩展插件写入扩展 ！ 分析](writing-an-analysis-extension-to-extend--analyze.md)

[**FA\_ENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extsfns/ns-extsfns-_fa_entry)

 

 






