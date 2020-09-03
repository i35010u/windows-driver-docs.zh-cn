---
title: BinPlace 命令行语法
description: BinPlace 在命令行中使用以下语法
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
ms.openlocfilehash: bbceafc768dcdba0aacfeebcc1d6ab3f76346755
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384395"
---
# <a name="binplace-command-line-syntax"></a>BinPlace 命令行语法


BinPlace 在命令行中使用以下语法：

```
    binplace [Options] File [ [Options] [@PlaceFile] File [...] ]
```

## <a name="span-idddk_binplace_command_line_syntax_toolsspanspan-idddk_binplace_command_line_syntax_toolsspanparameters"></a><span id="ddk_binplace_command_line_syntax_tools"></span><span id="DDK_BINPLACE_COMMAND_LINE_SYNTAX_TOOLS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
这可以包括以下任何开关。 开关前面应带有连字符 ( ) 或斜杠 (/) 。 可以在一个连字符或斜线后组合几个选项，但带有其他参数的选项后面应跟一个空格。 因此，以下两个命令是等效的：

```
binplace -q -k -g LCFile -v -s SymbolRoot File 
binplace -qkg LCFile -vs SymbolRoot File 
```

以下开关可用：

<span id="-a"></span><span id="-A"></span>**-a**  
导致 BinPlace 在放置符号文件时将其去除。 这会创建去除符号文件，其中包含公共符号，而不包含私有符号。 使用 **-a** 开关时，还必须使用 **-s** 和 **-x** 。 使用 **-a** 时，去除的符号文件将放在由 **-s *** * SymbolRoot 指定的路径中。 如果还存在 **-n ** * * FullSymbolRoot，则会将完整的符号文件放在 *FullSymbolRoot*中。 否则，它们将不会放在任何位置。

<span id="-b_ExtraSubdirectory"></span><span id="-b_extrasubdirectory"></span><span id="-B_EXTRASUBDIRECTORY"></span>**-b** *ExtraSubdirectory*  
使 BinPlace 将文件放在与平常不同的位置。 在串联根目标目录、类子目录以及正常的文件类型子目录后，BinPlace 会将 *ExtraSubdirectory* 附加到此路径，以创建最终的目标目录。 *ExtraSubdirectory* 不应以反斜杠开头或结尾。 有关更多详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-e"></span><span id="-E"></span>**-e**  
如果文件无法放置，会导致 BinPlace 继续执行。 默认情况下，发生此错误时，BinPlace 将退出。

<span id="-f"></span><span id="-F"></span>**-f**  
强制 BinPlace 放置一个文件，即使它覆盖了一个较新的文件。 默认情况下，当 BinPlace 尝试放置某个文件时，它将覆盖较旧的版本，但不会覆盖较新的版本。

<span id="-g_LCFile"></span><span id="-g_lcfile"></span><span id="-G_LCFILE"></span>**-g** *LCFile*  
导致 BinPlace 验证可执行文件。 *LCFile* 指定要用于此验证的本地化约束文件。

<span id="-h"></span><span id="-H"></span>**-h**  
导致 BinPlace 创建硬链接，而不是在放置文件时复制文件。 此选项仅在 NTFS 文件系统上可用。

<span id="-j"></span><span id="-J"></span>**-j**  
导致 BinPlace 在复制任何可执行文件之前验证正确的符号是否存在。 要使用此选项，SymChk 工具必须在你的路径中。  (SymChk 是 Windows 包调试工具的一部分。 有关详细信息，请参阅 [Windows 调试](../debugger/index.md) 。 ) 

<span id="-k"></span><span id="-K"></span>**-k**  
导致 BinPlace 保留文件属性。 默认情况下，BinPlace 将关闭存档属性。

<span id="-n_FullSymbolRoot"></span><span id="-n_fullsymbolroot"></span><span id="-N_FULLSYMBOLROOT"></span>**-n** *FullSymbolRoot*  
指定包含) 的公共和私有符号 (符号文件的完整符号文件的根目录。 这还需要 **-a**、 **-x**和 **-s** 开关。 有关更多详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-o_RootSubdirectory"></span><span id="-o_rootsubdirectory"></span><span id="-O_ROOTSUBDIRECTORY"></span>**-o** *RootSubdirectory*  
指定要使用的根目标目录的子目录。 创建目标目录时，将在根目标目录之后和类子目录之前插入 *RootSubdirectory* 。 有关更多详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-p_PlaceFile"></span><span id="-p_placefile"></span><span id="-P_PLACEFILE"></span>**-p** *PlaceFile*  
指定位置文件的路径和文件名。 如果未使用 **-p**开关，BinPlace 将使用名为* \\ tools \\placefil.txt*的位置。 有关位置文件内容的说明，请参阅 [**放置文件语法**](place-file-syntax.md) 。

**注意** **-P** 开关和位置文件现在已过时，不应使用。



<span id="-q"></span><span id="-Q"></span>**-q**  
禁止 BinPlace 使用日志文件。 如果省略 **-q** 开关，则将 BINPLACE 日志环境变量指定的文件用作 \_ 日志文件。

<span id="-r_RootDestinationPath"></span><span id="-r_rootdestinationpath"></span><span id="-R_ROOTDESTINATIONPATH"></span>**-r** *RootDestinationPath*  
指定根目标目录。 如果省略此值，则默认值由基于 \_ Itanium 的基于 \_ Itanium 的 \_ 计算机或基于 x64 的计算机上的 NT386TREE、NTIA64TREE 或 NTAMD64TREE 环境变量决定。 有关详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-s_SymbolRoot"></span><span id="-s_symbolroot"></span><span id="-S_SYMBOLROOT"></span>**-s** *SymbolRoot*  
指定符号文件的根目录。 如果同时使用了 **-a** 和 **-x** 开关，则将从符号文件中去除私有符号，并将去除的符号文件放在由 *SymbolRoot*指定的目录中。 如果要同时放置去除和完整符号文件，应使用-a-x-s SymbolRoot-n FullSymbolRoot。 有关更多详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-t"></span><span id="-T"></span>**-t**  
*测试模式*。 使用此开关时，不会复制任何文件，但 BinPlace 将显示警告和错误消息，就像它放入文件一样。 你可能还希望使用 **-v** 开关来增加消息的数量。

<span id="-u"></span><span id="-U"></span>**-u**  
导致 BinPlace 追加 \\ 到类子目录。 这对于分离单处理器 () 驱动程序很有用。 此外，每当使用此开关时，BinPlace 将不会拆分包含符号的可执行文件。 有关更多详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-v"></span><span id="-V"></span>**-v**  
*详细模式*。 导致 BinPlace 显示更详细的错误、警告和进度消息。

<span id="-w"></span><span id="-W"></span>**-w**  
导致 BinPlace 将 () 的 Windows 95 符号文件添加到符号树中。

<span id="-x"></span><span id="-X"></span>**-x**  
如果 BinPlace 遇到使用 *旧符号系统*的文件，此开关会使其删除可执行文件中的所有符号，并将此信息移到不同的符号文件中。 有关详细信息，请参阅 [符号文件系统](symbol-file-systems.md) 。 使用 **-x** 开关时，还必须使用 **-s** 和 **-a** 。

<span id="-y"></span><span id="-Y"></span>**-y**  
阻止 BinPlace 使用任何类子目录。 将仅从根目标目录和文件类型子目录创建目标目录。 有关详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-z"></span><span id="-Z"></span>**-z**  
取消 **-x** 开关。 如果对多个目标使用 BinPlace，可以使用 **BinPlace** *argumentsTarget1argumentsTarget2*形式的命令，因为命令行是从左到右进行分析的，所以， *Target1* 和 *Target2* 会受到不同参数的影响。  (参见下面) 的 "分析顺序" 部分。 如果遇到 **a-z 开关，** 则会取消任何上一个 **x** 开关的效果。

<span id="-ci_ReturnCode_Application_Argument_Argument__..._"></span><span id="-ci_returncode_application_argument_argument__..._"></span><span id="-CI_RETURNCODE_APPLICATION_ARGUMENT_ARGUMENT__..._"></span>**-ci** <em>ReturnCode</em>**，**<em>应用程序</em>**，**<em>参数</em>**，**<em>参数</em>**...**   
导致 BinPlace 使用自定义应用程序来验证所有可执行文件。 如果希望 BinPlace 使用其他应用程序进行验证，可以使用 **-ci** 开关。

如果此应用程序在可执行文件中发现错误，则*ReturnCode*应为此应用程序返回的值。 其他参数用于启动此应用程序。 它们必须用逗号分隔。 *应用程序* 指定程序的名称。 这可以后跟任意数量的命令行参数。 该程序将使用命令行启动，其中包括 *应用程序* ，后面跟有空格（而不是) 逗号）分隔的所有参数 (，最后以要检查的可执行文件的名称结束。

<span id="-_ARC"></span><span id="-_arc"></span>**-：圆弧**  
导致 BinPlace 仅放置设置了存档属性的文件。

<span id="-_DBG"></span><span id="-_dbg"></span>**-:D BG**  
阻止 BinPlace 放置 dbg 文件。 如果同时使用了 **-j** 开关，这会阻止 BinPlace 将指向 dbg 文件的二进制文件放入其中。 要使用此选项，SymChk 工具必须在你的路径中。  (SymChk 是 Windows 包调试工具的一部分。 有关详细信息，请参阅 [Windows 调试](../debugger/index.md) 。 ) 

<span id="-_DEST_ClassPath"></span><span id="-_dest_classpath"></span><span id="-_DEST_CLASSPATH"></span>**-:D est** *类路径*  
使 BinPlace 忽略位置文件并使用指定的 *类路径* 作为类子目录。 有关详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="-_LOGPDB"></span><span id="-_logpdb"></span>**-:LOGPDB**  
导致 BinPlace 将完整的 .pdb 路径包含在日志文件中。

<span id="-_REN_NewName"></span><span id="-_ren_newname"></span><span id="-_REN_NEWNAME"></span>**-： REN** *NewName*  
导致 BinPlace 重命名正在放置的文件。 初始文件名（包括扩展名）将替换为 *NewName*。  (如果原始文件是要拆分的可执行文件，则将为新的符号文件提供原始文件名加上扩展名。 ) 

<span id="-_TMF"></span><span id="-_tmf"></span>**-:TMF**  
使 BinPlace 通过从 PDB 符号文件中提取跟踪消息格式设置指令来 [) 文件创建跟踪消息 ( 格式](trace-message-format-file.md) 。 TMF 文件将放在由 BinPlace 跟踪 \_ 格式路径环境变量指定的目录中 \_ 。 请参阅 [BinPlace 宏和环境变量](binplace-macros-and-environment-variables.md)。

<span id="-ChangeAsmsToRetailForSymbols"></span><span id="-changeasmstoretailforsymbols"></span><span id="-CHANGEASMSTORETAILFORSYMBOLS"></span>**-ChangeAsmsToRetailForSymbols**  
导致 BinPlace 将字符串 "asm" 替换为字符串 "零售" （如果它出现在符号文件的目标目录中）。 有关更多详细信息，请参阅 [BinPlace 目标目录](binplace-destination-directories.md) 。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span>*文件*   
指定 BinPlace 将作用于的文件的完整路径和文件名。 可以列出任意数目的文件，由空格分隔。 如果路径和文件名包含空格，则必须用引号将路径和文件名引起来。

<span id="________PlaceFile______"></span><span id="________placefile______"></span><span id="________PLACEFILE______"></span>**@** <em>PlaceFile</em>   
如果任何文件名前面带有 at 符号 ( **@** ) ，则文件名表示位置文件的名称。 有关详细信息，请参阅下面的在文件中提供参数部分。

### <a name="span-idparsing_orderspanspan-idparsing_orderspanparsing-order"></a><span id="parsing_order"></span><span id="PARSING_ORDER"></span>分析顺序

BinPlace 从左到右分析命令行。 您可以指定多个选项，然后指定一个 *文件* 参数，然后选择 "新选项"，然后依次指定其他 *文件* 参数。 每次 BinPlace 遇到新的选项时，将采用该选项，替代前面提到的任何矛盾选项。 无论何时遇到 *文件* 说明符，它都将使用命令行上已遇到的累积选项来处理该文件。

### <a name="span-idsupplying_parameters_in_a_filespanspan-idsupplying_parameters_in_a_filespansupplying-parameters-in-a-file"></a><span id="supplying_parameters_in_a_file"></span><span id="SUPPLYING_PARAMETERS_IN_A_FILE"></span>在文件中提供参数

可以通过文本文件将参数传递给 BinPlace。 有两种方法可以实现此目的：

-   可以在 BINPLACE \_ 替代标志环境变量中指定文件名 \_ 。 在运行 BinPlace 时，将读取此文件，并将其内容用作参数。 此文件中的参数将在实际显示在 BinPlace 命令行上的参数之前进行分析。

-   你可以在 BinPlace 命令行上指定文件名，方法是使用 at 符号 ( ) 来指定文件名 **@** 。 如果 BinPlace 在其命令行中看到以该符号开头的字符串，则它将采用字符串，删除 at 符号，然后查找具有此名称的文件。 如果找到此文件，它会将其文本插入命令行中的位置，该位置与以 at 符号开头的原始参数的位置完全相同。 由于 BinPlace 从左到右分析参数，因此可以将此方法与多个 *文件* 实例一起使用，以便对每个文件使用 BinPlace，而无需每次都键入所有选项。  (如果未找到此文件，BinPlace 会将原始字符串（包括 at 符号）视为 *文件* 参数。 ) 