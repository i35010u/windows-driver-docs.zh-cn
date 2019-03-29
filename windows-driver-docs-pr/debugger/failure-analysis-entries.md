---
title: 故障分析项
description: DebugFailureAnalysis 对象具有故障分析项的集合。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1827ec250381d96a06f72955f679ecf7ec4fd25a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569460"
---
# <a name="failure-analysis-entries"></a>故障分析项


一个[ **DebugFailureAnalysis** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)对象具有故障分析项的集合。 有关详细信息，请参阅[失败分析条目、 标记和数据类型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)。

一个*无法分析项*(也称为*FA 条目*) 是以下之一：

-   [ **FA\_条目**](https://msdn.microsoft.com/library/windows/hardware/jj991808)结构
-   [ **FA\_条目**](https://msdn.microsoft.com/library/windows/hardware/jj991808)结构后, 跟一个数据块

**DataSize**的成员[ **FA\_条目**](https://msdn.microsoft.com/library/windows/hardware/jj991808)结构保留大小，以字节为单位的数据块。 如果没有数据块， **DataSize**等于 0。 **标记**的成员**FA\_条目**结构标识的 FA 项中存储的信息种类。 例如，标记**调试\_FLR\_检测错误\_代码**指示数据块的**FA\_条目**包含错误检查代码。

在某些情况下，没有必要的数据块的;由标记传达的信息。 例如， [ **FA\_条目**](https://msdn.microsoft.com/library/windows/hardware/jj991808)标记**调试\_FLR\_内核\_VERIFIER\_已启用**不有任何数据块。

每个标记是与一个中的数据类型相关联[ **FA\_条目\_类型**](https://msdn.microsoft.com/library/windows/hardware/jj991809)枚举。 例如，标记**调试\_FLR\_检测错误\_代码**的数据类型与关联**调试\_FA\_条目\_ULONG**. 若要确定标记的数据类型，请调用[ **GetType** ](https://msdn.microsoft.com/library/windows/hardware/jj991813)方法[IDebugFAEntryTags](https://msdn.microsoft.com/library/windows/hardware/jj983404)接口。

若要获取或设置一个 FA 条目的数据块，使用[ **IDebugFailureAnalysis2** ](https://msdn.microsoft.com/library/windows/hardware/jj983405)接口。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[分析扩展插件写入扩展 ！ 分析](writing-an-analysis-extension-to-extend--analyze.md)

[**FA\_ENTRY**](https://msdn.microsoft.com/library/windows/hardware/jj991808)

 

 






