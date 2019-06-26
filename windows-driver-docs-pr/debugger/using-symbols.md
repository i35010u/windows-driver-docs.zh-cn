---
title: 使用符号
description: 使用符号
ms.assetid: 1de1441f-b4d7-49e9-87ad-392a75b3d4be
keywords:
- 调试器引擎符号
- 符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46aca9704ee5a17e310f046187d6828eaf0f704b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368613"
---
# <a name="using-symbols"></a>使用符号


## <span id="ddk_symbols_dbx"></span><span id="DDK_SYMBOLS_DBX"></span>


有关概述符号，包括使用符号文件和符号服务器，请参阅[符号](symbols.md)。

### <a name="span-idsymbolnamesandlocationsspanspan-idsymbolnamesandlocationsspansymbol-names-and-locations"></a><span id="symbol_names_and_locations"></span><span id="SYMBOL_NAMES_AND_LOCATIONS"></span>符号的名称和位置

若要查找在给定名称的符号的位置，请使用[ **GetOffsetByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyname)。 若要指定符号名称所使用的语法的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

如果不知道确切的符号名称，或多个符号具有相同的名称， [ **StartSymbolMatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-startsymbolmatch)将开始搜索其名称与给定的模式匹配的符号。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

若要查找的给定其位置的符号名称，请使用[ **GetNameByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getnamebyoffset)。 若要在给定位置附近模块中查找的符号的名称，请使用[ **GetNearNamebyOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getnearnamebyoffset)。

**请注意**  只要有可能，限定的符号宽度的模块名称-例如**mymodule ！ 主要**。 否则，如果符号不存在 （例如，由于犯了输入错误），引擎将必须加载并搜索每个模块; 的符号这可以是一个缓慢的过程，尤其是对于内核模式调试。 如果符号名称已使用的模块名称限定的则引擎将仅需要搜索该模块的符号。

 

使用结构唯一标识一个符号[**调试\_模块\_AND\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_module_and_id)。 此结构由方法返回[ **GetSymbolEntriesByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyname)并[ **GetSymbolEntriesByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyoffset)，其搜索分别基于其名称和位置，符号。

该方法[ **GetSymbolEntryInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation)返回的符号的使用说明[**调试\_符号\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_entry)结构。

若要查找在结构中的字段的偏移量，请使用[ **GetFieldOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)。 若要查找的给定索引在结构中的字段名称，请使用[ **GetFieldName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getfieldname)。 若要查找给定其值的枚举常量的名称，请使用[ **GetConstantName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getconstantname)。

该方法[ **GetSymbolInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-getsymbolinformation)可以执行多个请求的符号信息。

### <a name="span-idsymboloptionsspanspan-idsymboloptionsspansymbol-options"></a><span id="symbol_options"></span><span id="SYMBOL_OPTIONS"></span>符号选项

选项控制如何加载和卸载符号的数。 有关这些选项的说明，请参阅[设置符号选项](symbol-options.md)。

符号选项可能会使用开启[ **AddSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-addsymboloptions)，并通过使用关闭[ **RemoveSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-removesymboloptions)。

[**GetSymbolOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymboloptions)返回当前符号选项。 若要同时设置符号的所有选项，请使用[ **SetSymbolOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setsymboloptions)。

### <a name="span-idreloadingsymbolsspanspan-idreloadingsymbolsspanreloading-symbols"></a><span id="reloading_symbols"></span><span id="RELOADING_SYMBOLS"></span>重新加载符号

加载符号文件之后, 该引擎在内部缓存中存储的符号信息。 若要刷新此缓存，请使用[**重新加载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-reload)。 这些符号将需要再次现在或更高版本时进行加载。

### <a name="span-idsyntheticsymbolsspanspan-idsyntheticsymbolsspan-synthetic-symbols"></a><span id="synthetic_symbols"></span><span id="SYNTHETIC_SYMBOLS"></span> 综合符号

*综合符号*是一种方式标记的任意地址以方便引用。 可以在任何现有模块中创建综合的符号。 该方法[ **AddSyntheticSymbol** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticsymbol)创建新的综合符号。 可以使用删除综合符号[ **RemoveSyntheticSymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticsymbol)。 重新加载模块的符号将删除与该模块相关联的所有综合符号。

### <a name="span-idsymbolpathspanspan-idsymbolpathspansymbol-path"></a><span id="symbol_path"></span><span id="SYMBOL_PATH"></span>符号路径

若要添加到符号路径的目录或符号服务器，请使用方法[ **AppendSymbolPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-appendsymbolpath)。 返回整个符号路径[ **GetSymbolPath** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolpath) ，可以使用更改[ **SetSymbolPath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols3-setsymbolpath)。

 

 





