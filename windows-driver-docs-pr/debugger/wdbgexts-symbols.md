---
title: WdbgExts 符号
description: WdbgExts 符号
ms.assetid: 7e1a1799-b87c-42cb-94ce-fbdc9a5ec973
keywords:
- WdbgExts 扩展符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e84d2f0573ab54d8a46e22484acc7ce742fd513d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524706"
---
# <a name="wdbgexts-symbols"></a>WdbgExts 符号


本主题提供概述的符号可以是操作使用 WdbgExts API。 有关使用中的符号的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[符号](symbols.md)中[调试器引擎概述](debugger-engine-overview.md)此文档的部分。

若要评估 MASM 或 c + + 表达式，使用函数[ **GetExpression** ](https://msdn.microsoft.com/library/windows/hardware/ff546683)或[ **GetExpressionEx**](https://msdn.microsoft.com/library/windows/hardware/ff546691)。

若要读取的结构中成员的值，使用[ **GetFieldData** ](https://msdn.microsoft.com/library/windows/hardware/ff546743)函数或，如果成员包含基元值[ **GetFieldValue** ](https://msdn.microsoft.com/library/windows/hardware/ff546781)可用。 若要确定目标的内存中的符号的实例大小，请使用[ **GetTypeSize** ](https://msdn.microsoft.com/library/windows/hardware/ff549446)函数。

若要查找在结构中成员的偏移量，请使用[ **GetFieldOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff546758)函数。

若要读取结构中的多个成员，首先使用[ **InitTypeRead** ](https://msdn.microsoft.com/library/windows/hardware/ff550953)函数初始化结构。 然后，可以使用[ **ReadField** ](https://msdn.microsoft.com/library/windows/hardware/ff553539)函数一次小于或等于 8 个字节一个读取大小具有的成员。 对于在物理内存中结构地址，使用[ **InitTypeReadPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff550957)函数而不是**InitTypeRead**。

有两个函数，可用于循环访问链接列表。 使用列表的双向链接列表\_ENTRY32 或列表\_ENTRY64 结构，该函数[ **ReadListEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff553585)可用于查找下一步和上一个条目。 该函数[ **ListType** ](https://msdn.microsoft.com/library/windows/hardware/ff551988)将循环访问链接列表中的所有项并为每个条目调用回调函数。

若要在目标计算机的内存中查找指定地址附近的符号，请使用[ **GetSymbol** ](https://msdn.microsoft.com/library/windows/hardware/ff548447)函数。

若要从调试器引擎的缓存中删除所有符号信息，请使用[ **ReloadSymbols** ](https://msdn.microsoft.com/library/windows/hardware/ff554381)函数。 若要读取或更改的符号路径，用于搜索符号文件，请使用[ **GetSetSympath** ](https://msdn.microsoft.com/library/windows/hardware/ff548291)函数。

可以通过执行由调试器引擎提供的几乎所有符号 operations [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_转储\_符号\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff550906)。 但是，而且非常灵活的函数，它高级，我们建议使用更高版本的更简单函数，在适用的情况。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

功能更强大的符号 API，请参阅[使用符号](using-symbols.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





