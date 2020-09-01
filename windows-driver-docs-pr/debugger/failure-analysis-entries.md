---
title: 故障分析项
description: DebugFailureAnalysis 对象具有失败分析条目的集合。
ms.assetid: 759DE159-F2A8-4BB1-AAF5-B2B91C4F91B0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e0fa704e70ba8bda7f21750bbe1fdebc5ebe76e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211161"
---
# <a name="failure-analysis-entries"></a>故障分析项


[**DebugFailureAnalysis**](/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2)对象具有失败分析条目的集合。 有关详细信息，请参阅 [故障分析条目、标记和数据类型](writing-an-analysis-extension-to-extend--analyze.md#failure-analysis-entries-tags-and-data-types)。

*失败分析条目* (也称为*FA 条目*) 为以下之一：

-   [**FA \_ 条目**](/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)结构
-   一个 [**FA \_ 条目**](/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry) 结构，后跟一个数据块

[**FA \_ 条目**](/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)结构的**DataSize**成员保存数据块的大小（以字节为单位）。 如果没有数据块，则 **DataSize** 等于0。 **Fa \_ 条目**结构的**标记**成员标识在 fa 条目中存储的信息的类型。 例如，标记 **DEBUG \_ FLR \_ 错误检查 \_ 代码** 指示 **FA \_ 条目** 的数据块包含 bug 检查代码。

在某些情况下，不需要数据块;所有信息都由标记传达。 例如，启用了 tag **DEBUG \_ FLR \_ 内核 \_ 验证 \_ **程序的[**FA \_ 条目**](/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)没有数据块。

每个标记都与 [**FA \_ 项 \_ 类型**](/windows-hardware/drivers/ddi/extsfns/ne-extsfns-_fa_entry_type) 枚举中的一个数据类型相关联。 例如，tag **debug \_ FLR \_ 检测错误 \_ 代码** 与数据类型 " **调试" \_ FA \_ 条目 \_ ULONG**相关联。 若要确定标记的数据类型，请调用[IDebugFAEntryTags](/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfaentrytags)接口的[**GetType**](/windows-hardware/drivers/ddi/extsfns/nf-extsfns-idebugfaentrytags-gettype)方法。

若要获取或设置 FA 条目的数据块，请使用 [**IDebugFailureAnalysis2**](/windows-hardware/drivers/ddi/extsfns/nn-extsfns-idebugfailureanalysis2) 接口。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[编写分析扩展插件以扩展 !analyze](writing-an-analysis-extension-to-extend--analyze.md)

[**FA \_ 条目**](/windows-hardware/drivers/ddi/extsfns/ns-extsfns-_fa_entry)

 

