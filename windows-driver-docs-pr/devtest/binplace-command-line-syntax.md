---
title: BinPlace 命令行语法
description: BinPlace 在命令行使用以下语法
ms.assetid: 8489b7ae-3e3b-41d5-b9a6-0b69aa92087e
keywords:
- BinPlace 命令行语法驱动程序开发工具
topic_type:
- apiref
api_name:
- BinPlace Command-Line Syntax
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f30c322ba0ab87ed2c47e38afe96a6be1f203cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381888"
---
# <a name="binplace-command-line-syntax"></a>BinPlace 命令行语法


BinPlace 在命令行使用以下语法：

```
    binplace [Options] File [ [Options] [@PlaceFile] File [...] ]
```

## <a name="span-idddkbinplacecommandlinesyntaxtoolsspanspan-idddkbinplacecommandlinesyntaxtoolsspanparameters"></a><span id="ddk_binplace_command_line_syntax_tools"></span><span id="DDK_BINPLACE_COMMAND_LINE_SYNTAX_TOOLS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
这可能包括任何以下开关。 开关的前面应带有连字符 （-） 或斜杠 （/）。 可以将多个选项组合在一个连字符或正斜杠后, 但需要使用其他参数的选项应跟一个空格。 因此，以下两个命令是等效的：

```
binplace -q -k -g LCFile -v -s SymbolRoot File 
binplace -qkg LCFile -vs SymbolRoot File 
```

提供了以下开关：

<span id="-a"></span><span id="-A"></span>**-a**  
导致 BinPlace 时在被放入带符号文件中去除私有符号。 这将创建包含公共符号，但不是能是专用的符号的去除的符号文件。 使用时 **-a**开关，则必须使用 **-s**并 **-x**也。 当 **-a**使用时，符号文件将放置在指定的路径中去除 **-s * * * SymbolRoot*。 如果 **-n * * * FullSymbolRoot*还存在完整的符号文件将被放置在*FullSymbolRoot*。 否则，它们不会发出任何位置。

<span id="-b_ExtraSubdirectory"></span><span id="-b_extrasubdirectory"></span><span id="-B_EXTRASUBDIRECTORY"></span>**-b** *ExtraSubdirectory*  
导致 BinPlace 若要将文件放在长于平常的其他位置。 像往常一样串联根目标目录、 类子目录和文件类型子目录之后, BinPlace 然后追加*ExtraSubdirectory*向此路径来创建最终的目标目录。 *ExtraSubdirectory*应既开头不以反斜杠结尾。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)的更多详细信息。

<span id="-e"></span><span id="-E"></span>**-e**  
导致 BinPlace 继续执行，则不能放置一个文件。 默认情况下，此错误发生时将退出 BinPlace。

<span id="-f"></span><span id="-F"></span>**-f**  
强制 BinPlace 放置一个文件，即使它覆盖较新的文件。 默认情况下，当 BinPlace 尝试将文件，它将覆盖较旧版本但不是会覆盖较新版本。

<span id="-g_LCFile"></span><span id="-g_lcfile"></span><span id="-G_LCFILE"></span>**-g** *LCFile*  
若要验证的可执行文件的原因 BinPlace。 *LCFile*指定要用于此验证的本地化约束文件。

<span id="-h"></span><span id="-H"></span>**-h**  
导致 BinPlace 创建硬链接而不是复制该文件时将文件放。 此选项才可用 NTFS 文件系统上。

<span id="-j"></span><span id="-J"></span>**-j**  
若要验证正确的符号复制任何可执行文件之前存在的原因 BinPlace。 对于要使用此选项，SymChk 工具必须在你的路径。 （SymChk 是有关 Windows 调试工具软件包的一部分。 请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)有关详细信息。)

<span id="-k"></span><span id="-K"></span>**-k**  
导致 BinPlace 来保留文件属性。 默认情况下，BinPlace 将关闭的存档特性。

<span id="-n_FullSymbolRoot"></span><span id="-n_fullsymbolroot"></span><span id="-N_FULLSYMBOLROOT"></span>**-n** *FullSymbolRoot*  
指定完整的符号文件 （包含公钥和私钥的符号的符号文件） 的根目录。 这需要 **-a**， **-x**，并 **-s**也开关。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)的更多详细信息。

<span id="-o_RootSubdirectory"></span><span id="-o_rootsubdirectory"></span><span id="-O_ROOTSUBDIRECTORY"></span>**-o** *RootSubdirectory*  
指定要使用的根目标目录的子目录。 创建目标目录时， *RootSubdirectory*根目标目录之后和类子目录之前将插入。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)的更多详细信息。

<span id="-p_PlaceFile"></span><span id="-p_placefile"></span><span id="-P_PLACEFILE"></span>**-p** *PlaceFile*  
指定位置文件的路径和文件。 如果 **-p**不使用开关、 BinPlace 使用名为的位置*\\工具\\placefil.txt*。 请参阅[**位置文件语法**](place-file-syntax.md)位置文件的内容的说明。

**请注意** **-p**切换，并将文件现在已过时，并且不应使用。



<span id="-q"></span><span id="-Q"></span>**-q**  
防止 BinPlace 使用日志文件。 如果 **-q** BINPLACE 指定的文件省略开关\_日志环境变量用作日志文件。

<span id="-r_RootDestinationPath"></span><span id="-r_rootdestinationpath"></span><span id="-R_ROOTDESTINATIONPATH"></span>**-r** *RootDestinationPath*  
指定的根目标目录。 如果省略，默认值由\_NT386TREE， \_NTIA64TREE，或\_NTAMD64TREE 环境变量在基于 x86 的、 基于 Itanium 或基于 x64 的计算机上，分别。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)有关详细信息。

<span id="-s_SymbolRoot"></span><span id="-s_symbolroot"></span><span id="-S_SYMBOLROOT"></span>**-s** *SymbolRoot*  
指定符号文件的根目录。 如果 **-a**并 **-x**还使用开关、 将带符号文件，去除私有符号和去除的符号文件将位于指定的目录*SymbolRoot*. 如果你想要将这两个去除和完整符号文件，则应使用-a-x-s SymbolRoot-n FullSymbolRoot。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)的更多详细信息。

<span id="-t"></span><span id="-T"></span>**-t**  
*测试模式下*。 如果使用此开关，没有文件将被复制，但 BinPlace 将显示警告和错误消息，如同已将文件放。 您可能想要使用 **-v**开关以增加消息数。

<span id="-u"></span><span id="-U"></span>**-u**  
导致要追加的 BinPlace\\最多的类的子目录。 这可用于将分离出来单处理器 (UP) 驱动程序。 此外，只要使用此开关，BinPlace 将不会拆分包含符号的可执行文件。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)的更多详细信息。

<span id="-v"></span><span id="-V"></span>**-v**  
*详细模式*。 导致 BinPlace 以显示更详细的错误、 警告和进度消息。

<span id="-w"></span><span id="-W"></span>**-w**  
若要将 Windows 95 符号文件 (.sym) 添加到符号树的原因 BinPlace。

<span id="-x"></span><span id="-X"></span>**-x**  
如果使用的文件时遇到 BinPlace*旧符号系统*，此开关会导致它从可执行文件中删除所有符号和移动这些单独的符号文件的信息。 请参阅[符号文件系统](symbol-file-systems.md)有关详细信息。 使用时 **-x**开关，则必须使用 **-s**并 **-a**也。

<span id="-y"></span><span id="-Y"></span>**-y**  
防止 BinPlace 使用类的任何子目录。 将仅从根目标目录和文件类型子目录创建目标目录。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)有关详细信息。

<span id="-z"></span><span id="-Z"></span>**-z**  
取消 **-x**切换。 如果要在多个目标上使用 BinPlace--可以使用格式的命令这会很有用**binplace** *argumentsTarget1argumentsTarget2*，由于命令行分析从左到右，*Target1*并*Target2*将受到不同的参数。 （请参阅下面分析顺序部分）。 如果**z**遇到开关，这将取消以前所有的效果 **-x**切换。

<span id="-ci_ReturnCode_Application_Argument_Argument__..._"></span><span id="-ci_returncode_application_argument_argument__..._"></span><span id="-CI_RETURNCODE_APPLICATION_ARGUMENT_ARGUMENT__..._"></span>**-ci** <em>ReturnCode</em>**，**<em>应用程序</em>**，**<em>参数</em>**，**<em>自变量</em>**，** ...   
若要使用自定义应用程序来验证所有可执行文件的原因 BinPlace。 可以使用 **-ci** ，如果你想要使用其他一些应用程序能够在执行其验证 BinPlace 切换。

*ReturnCode*应将返回此应用程序中，如果它在可执行文件中发现错误的值。 其他参数用于启动此应用程序。 这些必须所有逗号分隔。 *应用程序*指定的程序的名称。 随后可以出现任意数量的命令行参数。 该程序将启动包含的命令行*应用程序*跟 （用空格而不用逗号分隔），所有自变量和要检查的可执行文件的名称，最后末尾。

<span id="-_ARC"></span><span id="-_arc"></span>**-:ARC**  
导致 BinPlace 仅放置其存档属性设置的文件。

<span id="-_DBG"></span><span id="-_dbg"></span>**-:DBG**  
防止 BinPlace 放置.dbg 文件。 如果 **-j**还使用开关，这将防止 BinPlace 放置指向.dbg 文件的二进制文件。 对于要使用此选项，SymChk 工具必须在你的路径。 （SymChk 是有关 Windows 调试工具软件包的一部分。 请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)有关详细信息。)

<span id="-_DEST_ClassPath"></span><span id="-_dest_classpath"></span><span id="-_DEST_CLASSPATH"></span>**-:DEST** *ClassPath*  
将导致忽略位置文件并使用指定的 BinPlace *ClassPath*作为类的子目录。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)有关详细信息。

<span id="-_LOGPDB"></span><span id="-_logpdb"></span>**-:LOGPDB**  
若要在日志文件中包含完整的.pdb 路径的原因 BinPlace。

<span id="-_REN_NewName"></span><span id="-_ren_newname"></span><span id="-_REN_NEWNAME"></span>**-:REN** *NewName*  
若要重命名正在放置的文件的原因 BinPlace。 原始文件名，包括扩展，将会被*NewName*。 （如果原始文件将被拆分的可执行文件，新的符号文件将提供的原始文件名加上扩展.dbg。）

<span id="-_TMF"></span><span id="-_tmf"></span>**-:TMF**  
会导致创建 BinPlace[跟踪消息格式 (.tmf) 文件](trace-message-format-file.md)通过提取跟踪消息设置格式的 PDB 符号文件中的说明。 TMF 文件将位于 BinPlace 跟踪指定的目录\_格式\_PATH 环境变量。 请参阅[BinPlace 宏和环境变量](binplace-macros-and-environment-variables.md)。

<span id="-ChangeAsmsToRetailForSymbols"></span><span id="-changeasmstoretailforsymbols"></span><span id="-CHANGEASMSTORETAILFORSYMBOLS"></span>**-ChangeAsmsToRetailForSymbols**  
如果会导致 BinPlace 来的字符串替换为"asm"字符串"零售"符号文件的目标目录中出现。 请参阅[BinPlace 目标目录](binplace-destination-directories.md)的更多详细信息。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span> *文件*   
指定 BinPlace 将作用于的文件的完整路径和文件名。 可以列出任意数量的空格分隔的文件。 如果路径和文件名称包含空格，必须将路径和文件名称用引号引起来。

<span id="________PlaceFile______"></span><span id="________placefile______"></span><span id="________PLACEFILE______"></span> **@**<em>PlaceFile</em>   
如果任何文件名前面的 at 符号 ( **@** )，该文件名表示位置文件的名称。 有关详细信息，请参阅下面文件部分中提供的参数。

### <a name="span-idparsingorderspanspan-idparsingorderspanparsing-order"></a><span id="parsing_order"></span><span id="PARSING_ORDER"></span>分析顺序

BinPlace 分析命令行从左到右。 可以指定多个选项，则*文件*参数，则新的选项，则另一个*文件*参数，等等。 每当 BinPlace 遇到新的选项，它将被采用，重写任何先前已见到清楚的选项。 每当遇到*文件*说明符，它将处理命令行上使用的累计的选项已经遇到了该文件。

### <a name="span-idsupplyingparametersinafilespanspan-idsupplyingparametersinafilespansupplying-parameters-in-a-file"></a><span id="supplying_parameters_in_a_file"></span><span id="SUPPLYING_PARAMETERS_IN_A_FILE"></span>提供的文件中的参数

就可以从文本文件将参数传递给 BinPlace。 有两种方法来执行此操作：

-   您可以指定文件名称中 BINPLACE\_重写\_标志环境变量。 此文件将读取和 BinPlace 运行时作为参数使用其内容。 此文件中的参数将分析之前实际出现在 BinPlace 命令行的参数。

-   可以在 BinPlace 命令行上指定文件名称，由前加上 at 符号 ( **@** )。 当 BinPlace 会在其命令行上看到该符号开头的字符串时，它将采用字符串时，删除的登录，以及然后查找具有此名称的文件。 如果它找到此文件，它会将其文本插入到命令行处的位置的原始参数开头的 at 符号曾。 因为 BinPlace 分析从左到右的参数，您可以使用此技术的多个实例以及*文件*若要使用每个不同选项的多个文件上使用 BinPlace，而无需键入所有选项每次。 (如果找不到此文件，BinPlace 会将原始字符串，其中包括 at 符号，作为*文件*参数。)









