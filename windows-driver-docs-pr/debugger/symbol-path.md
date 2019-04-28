---
title: Windows 调试器的符号路径
description: 符号路径指定的 Windows 调试器 （WinDbg、 KD、 CDB、 NTST） 查找符号文件的位置。
ms.assetid: 705df98f-717f-40ad-a424-101826970691
keywords: 符号文件和路径，符号，延迟符号加载、 延迟的符号加载、 符号路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b9b2751df0473c1ddf8f840aa6b705b4de435f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335487"
---
# <a name="symbol-path-for-windows-debuggers"></a>Windows 调试器的符号路径


符号路径指定的 Windows 调试器 （WinDbg、 KD、 CDB、 NTST） 查找符号文件的位置。 有关符号和符号文件的详细信息，请参阅[符号](symbols.md)。

一些编译器 （如 Microsoft Visual Studio) 将符号文件放入二进制文件所在的目录。 符号文件和检查二进制文件包含路径和文件名称信息。 此信息经常使调试器能够自动找到符号文件。 如果你正在调试可执行文件生成计算机上的用户模式进程和符号文件仍处于其原始位置，调试器可以找到符号文件，而无需您设置符号路径。

在大多数其他情况下，必须设置符号路径以指向你的符号文件位置。

## <a name="span-idsymbolpathsyntaxspanspan-idsymbolpathsyntaxspanspan-idsymbolpathsyntaxspansymbol-path-syntax"></a><span id="Symbol_Path_Syntax"></span><span id="symbol_path_syntax"></span><span id="SYMBOL_PATH_SYNTAX"></span>符号路径语法


调试器的符号路径是包含多个目录路径，之间用分号分隔的字符串。

支持相对路径。 但是，除非您始终从相同的目录启动调试器，您应添加驱动器号或网络共享每个路径之前。 此外支持网络共享。

符号路径中每个目录，调试器在三个目录中查找。 例如，如果符号路径中包含`c:\MyDir`目录中，并使调试器寻找 DLL 的符号信息、 调试器首先查看`c:\MyDir\symbols\dll`，然后在`c:\MyDir\dll`，最后在`c:\MyDir`。 然后，调试器符号路径中每个目录重复此过程。 最后，调试器查找当前目录中，然后使用在当前目录中`..\dll`追加到它。 (调试器追加`..\dll`， `..\exe` ，或`..\sys`，取决于正在调试的二进制文件。)

符号文件具有日期和时间戳。 无需担心调试器将使用第一次可能会发现此序列中的错误符号。 它始终会查找与正在调试的二进制文件的时间戳匹配的符号。 有关详细信息的响应时符号文件不可用，请参阅[补偿的符号匹配问题](matching-symbol-names.md)。

设置符号路径的一种方法是通过输入[ **.sympath** ](-sympath--set-symbol-path-.md)命令。 有关其他方式来设置符号路径，请参阅[控制符号路径](#controlling-the-symbol-path)本主题中更高版本。

## <a name="span-idcachingsymbolslocallyspanspan-idcachingsymbolslocallyspanspan-idcachingsymbolslocallyspancaching-symbols-locally"></a><span id="Caching_Symbols_Locally"></span><span id="caching_symbols_locally"></span><span id="CACHING_SYMBOLS_LOCALLY"></span>本地缓存符号


我们强烈建议你始终缓存您的本地符号。 一种方法符号缓存到本地是包括`cache*;`或`cache*localsymbolcache;*`符号路径中。

如果包含字符串`cache*;`在你的符号路径，此字符串的右侧会显示任何元素中加载符号存储在本地计算机上的默认符号缓存目录中。 例如，以下命令将指示调试器从网络共享获取符号`\\someshare`并缓存在本地计算机上的默认位置中的符号。

```dbgcmd
.sympath cache*;\\someshare
```

如果包含字符串`cache*localsymbolcache;`在您的符号路径，此字符串的右侧会显示任何元素中加载符号存储在*localsymbolcache*目录。

例如，以下命令将指示调试器从网络共享获取符号`\\someshare`缓存中的符号和`c:\MySymbols`目录。

```dbgcmd
.sympath cache*c:\MySymbols;\\someshare
```

## <a name="span-idusingasymbolserverspanspan-idusingasymbolserverspanspan-idusingasymbolserverspanusing-a-symbol-server"></a><span id="Using_a_Symbol_Server"></span><span id="using_a_symbol_server"></span><span id="USING_A_SYMBOL_SERVER"></span>使用符号服务器


如果连接到 Internet 或公司网络，访问符号的最有效方法是使用符号服务器。 还可以通过使用符号服务器`srv*`， `srv*symbolstore`，或`srv*localsymbolcache*symbolstore`符号路径中的字符串。

如果包含字符串`srv*`在符号路径中，调试器使用符号服务器获取符号从默认符号存储区。 例如，以下命令指示调试器使用符号服务器从默认符号存储区获取的符号。 这些符号不会缓存在本地计算机上。

```dbgcmd
.sympath srv*
```

如果包含字符串`srv*symbolstore`在您的符号路径，调试器使用符号服务器获取已从符号*symbolstore*存储。 例如，以下命令将指示调试器使用符号服务器获取符号从符号存储 https://msdl.microsoft.com/download/symbols。 这些符号不会缓存在本地计算机上。

```dbgcmd
.sympath srv*https://msdl.microsoft.com/download/symbols
```

如果包含字符串`srv*localcache*symbolstore`在您的符号路径，调试器使用符号服务器获取已从符号*symbolstore*存储，并将其在缓存*localcache*目录。 例如，以下命令将指示调试器使用符号服务器获取符号从符号存储 https://msdl.microsoft.com/download/symbols缓存中的符号和`c:\MyServerSymbols`。

```dbgcmd
.sympath srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

如果您手动设置符号的计算机上有一个目录，不要使用该目录作为缓存符号从符号服务器获取。 相反，使用两个不同的目录。 例如，可以手动设置中的符号`c:\MyRegularSymbols`并指定`c:\MyServerSymbols`作为从服务器获取的符号的缓存。 下面的示例演示如何在您的符号路径中指定这两个目录。

```dbgcmd
.sympath c:\MyRegularSymbols;srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

符号服务器的详细信息，请参阅[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)。

## <a name="span-idcombiningcacheandsrvspanspan-idcombiningcacheandsrvspanspan-idcombiningcacheandsrvspancombining-cache-and-srv"></a><span id="Combining_cache__and_srv_"></span><span id="combining_cache__and_srv_"></span><span id="COMBINING_CACHE__AND_SRV_"></span>合并缓存\*和 srv\*


如果包含字符串`cache*;`在你的符号路径，此字符串的右侧会显示任何元素中加载符号存储在本地计算机上的默认符号缓存目录中。 例如，以下命令将指示调试器使用符号服务器获取从存储在符号 https://msdl.microsoft.com/download/symbols并缓存在默认符号缓存目录中。

```dbgcmd
.sympath cache*;srv*https://msdl.microsoft.com/download/symbols
```

如果包含字符串`cache*localsymbolcache;`在您的符号路径，此字符串的右侧会显示任何元素中加载符号存储在*localsymbolcache*目录。

例如，以下命令将指示调试器使用符号服务器获取从存储在符号 https://msdl.microsoft.com/download/symbols缓存中的符号和`c:\MySymbols`目录。

```dbgcmd
.sympath cache*c:\MySymbols;srv*https://msdl.microsoft.com/download/symbols
```

## <a name="span-idusingagestoretoreducethecachesizespanspan-idusingagestoretoreducethecachesizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小


若要删除早于指定日期的缓存的文件，或若要删除生成缓存的大小小于指定的量足够旧文件，您可以使用 AgeStore 工具。 这很有用，如果你的下游存储太大。 有关详细信息，请参阅[AgeStore](agestore.md)。

有关符号服务器和符号存储区的详细信息，请参阅[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)。

## <a name="span-idlazysymbolloadingspanspan-idlazysymbolloadingspanlazy-symbol-loading"></a><span id="lazy_symbol_loading"></span><span id="LAZY_SYMBOL_LOADING"></span>延迟的符号加载


调试器的默认行为是使用*延迟符号加载*(也称为*延迟的符号加载*)。 这种加载意味着除非需要，还未加载符号。

如果更改符号路径，例如通过使用[ `.sympath` ](-sympath--set-symbol-path-.md)命令、 所有已加载模块导出的符号与延迟重新加载。

使用完整的 PDB 符号的模块的符号将延迟重新加载新的路径不能再包含用于加载 PDB 符号的原始路径。 如果新路径仍包含 PDB 符号文件的原始路径，这些符号将不会延迟重新加载。

有关延迟符号加载详细信息，请参阅[延迟的符号加载](deferred-symbol-loading.md)。

你可以关闭延迟符号加载 CDB 和 KD 中通过使用`-s`[命令行选项](command-line-options.md)。 您也可以使用强制符号加载`ld` [ **（加载符号）** ](ld--load-symbols-.md)命令或通过使用`.reload` [ **（重新加载模块）**](-reload--reload-module-.md)命令和`/f`选项。

## <span id="ddk_symbol_path_dbg"></span><span id="DDK_SYMBOL_PATH_DBG"></span>


### <a name="span-idcontrolling-the-symbol-pathspanspan-idcontrolling-the-symbol-pathspancontrolling-the-symbol-path"></a><span id="controlling-the-symbol-path"></span><span id="CONTROLLING-THE-SYMBOL-PATH"></span>控制符号路径

若要控制的符号路径，可以执行下列任一操作：

-   使用[ `.sympath` ](-sympath--set-symbol-path-.md)命令以显示、 设置、 更改或追加到路径。 `.symfix` [ **（设置符号存储区路径）** ](-symfix--set-symbol-store-path-.md)命令是类似于`.sympath`，但会将你键入一些内容。

-   启动调试器之前，请使用`_NT_SYMBOL_PATH`并`_NT_ALT_SYMBOL_PATH`[环境变量](environment-variables.md)设置的路径。 符号路径创建通过追加`_NT_SYMBOL_PATH`后`_NT_ALT_SYMBOL_PATH`。 (通常情况下，将路径设置通过`_NT_SYMBOL_PATH`。 但是，你可能想要使用`_NT_ALT_SYMBOL_PATH`重写这些设置，在特殊情况下，此类像具有共享的符号文件的专用版本。)如果尝试添加无效目录通过这些环境变量，调试器将忽略此目录。

-   当您启动调试器时，使用`-y`[命令行选项](command-line-options.md)设置的路径。

-   (仅 WinDbg)使用[文件 |符号文件路径](file---symbol-file-path.md)命令或按`CTRL+S`显示，请设置、 更改或追加到路径。

如果您使用`-sins`[命令行选项](command-line-options.md)，调试程序忽略符号路径环境变量。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[高级的 SymSrv 用途](advanced-symsrv-use.md)

 

 

