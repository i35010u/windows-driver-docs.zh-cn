---
title: WdbgExts 符号
description: WdbgExts 符号
keywords:
- WdbgExts 扩展，符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74089fc20a5657bd79f84b4605823e5787f00ced
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787669"
---
# <a name="wdbgexts-symbols"></a>WdbgExts 符号


本主题简要概述了如何使用 WdbgExts API 来操作符号。 有关在[调试器引擎](introduction.md#debugger-engine)中使用符号的概述，请参阅本文档的 "[调试器引擎概述](debugger-engine-overview.md)" 部分中的[符号](symbols.md)。

若要评估 MASM 或 c + + 表达式，请使用函数 [**system.componentmodel.design.serialization.codedomserializerbase.getexpression**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_get_expression) 或 [**GetExpressionEx**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getexpressionex)。

若要读取结构中成员的值，请使用 [**GetFieldData**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getfielddata) 函数，如果该成员包含基元值，则可以使用 [**GetFieldValue**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getfieldvalue) 。 若要确定某个符号在目标内存中的实例的大小，请使用 [**GetTypeSize**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-gettypesize) 函数。

若要在结构中查找成员的偏移量，请使用 [**GetFieldOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset) 函数。

若要读取结构中的多个成员，请首先使用 [**InitTypeRead**](/previous-versions/ff550953(v=vs.85)) 函数来初始化该结构。 然后，可以使用 [**ReadField**](/previous-versions/ff553539(v=vs.85)) 函数每次读取一个大小小于或等于8个字节的成员。 对于物理内存中的结构地址，请使用 [**InitTypeReadPhysical**](/previous-versions/ff550957(v=vs.85)) 函数而不是 **InitTypeRead**。

可以使用两个函数循环访问链接列表。 对于使用 LIST \_ ENTRY32 或 list ENTRY64 结构的双向链接列表 \_ ，可使用函数 [**ReadListEntry**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readlistentry) 查找下一个和上一个条目。 函数 [**ListType**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-listtype) 将循环访问链接列表中的所有条目，并为每个条目调用回调函数。

若要在目标内存中查找指定地址附近的符号，请使用 [**GetSymbol**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_get_symbol) 函数。

若要删除调试器引擎缓存中的所有符号信息，请使用 [**ReloadSymbols**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-reloadsymbols) 函数。 若要读取或更改符号路径（用于搜索符号文件），请使用 [**GetSetSympath**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getsetsympath) 函数。

调试器引擎提供的几乎所有符号操作都可以使用 [**Ioctl**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine) 操作 [**IG \_ 转储 \_ 符号 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)来执行。 但是，尽管这是一个非常灵活的函数，但它是高级的，我们建议你在适用的情况下使用上述更简单的函数。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关更强大的符号 API，请参阅本文档中的使用[调试器引擎 API](using-the-debugger-engine-api.md)使用[符号](using-symbols.md)部分。

 

