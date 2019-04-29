---
title: 使用 SymChk
description: 使用 SymChk
ms.assetid: 60c3df99-a842-4e46-a504-8e2b54030eef
keywords:
- SymChk，使用
ms.date: 10/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de2c5a15563aa81d706f4b6bd0feb24b564c4fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390824"
---
# <a name="using-symchk"></a>使用 SymChk


## <span id="ddk_using_symchk_dtoolq"></span><span id="DDK_USING_SYMCHK_DTOOLQ"></span>

SymChk 的基本语法如下所示：

```console
symchk [/r] FileNames /s SymbolPath 
```

*文件名*指定需要其符号的一个或多个程序文件。 如果*文件名*是一个目录并 **/r**使用标志，此目录是浏览以递归方式，SymChk 将尝试找到符号的所有程序在此目录树中的文件。 *SymbolPath*指定 SymChk 将搜索符号。

有更多的命令行选项。 有关完整列表，请参阅[SymChk 命令行选项](symchk-command-line-options.md)。

### <a name="obtaining-symchk"></a>获取 symchk

Symchk，与其他调试工具一样作为的一部分提供调试器。 有关详细信息，请参阅[的 Windows 中下载调试的工具](debugger-download-tools.md)。

调试工具在安装后，symchk 现已推出适用于 64 位 Windows 的此目录。

C:\\程序文件 (x86)\\Windows 工具包\\10\\调试器\\x64

### <a name="example-usage"></a>示例用法

指定的符号路径可以包含任意数量的本地目录、 UNC 目录或符号服务器。 本地目录和 UNC 目录不是以递归方式搜索。 搜索指定的目录和子目录基于可执行文件的扩展名。 例如，查询

```console
symchk thisdriver.sys /s g:\symbols 
```

将搜索 g:\\mysymbols 和 g:\\mysymbols\\sys。


可以使用以下语法之一作为符号路径的一部分指定符号服务器：

```console
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

这是非常类似于在调试器的符号路径中使用符号服务器。 有关详细信息，请参阅[使用符号服务器和符号存储区](symbol-stores-and-symbol-servers.md)。

如果指定下游存储，则 SymChk 将使发现的符号服务器，并将其放在下游存储区中的所有有效的符号文件的副本。 下游复制完整的匹配项的唯一符号文件。

查询符号服务器之前将 SymChk 始终搜索下游应用商店。 因此，你应小心地使用下游应用商店，当其他人保留符号存储区时。 如果一次运行 SymChk 并找到符号文件时，它将复制到下游应用商店。 如果您然后 SymChk 之后再次运行这些文件已被更改或删除在符号存储区上，SymChk 将无法发现这一事实，因为它会发现它查找的内容对下游存储和查看无需再。

**请注意**   SymChk 始终使用 SymSrv (Symsrv.dll) 作为其符号服务器 DLL。 另一方面，如果有可用调试程序可以选择 SymSrv 以外的 DLL 的符号服务器。 （SymSrv 是有关 Windows 调试工具软件包中包含的符号服务器。）
 

### <a name="span-idusingsymchktodeterminewhethersymbolsareprivateorpublicspanspan-idusingsymchktodeterminewhethersymbolsareprivateorpublicspanspan-idusingsymchktodeterminewhethersymbolsareprivateorpublicspanusing-symchk-to-determine-whether-symbols-are-private-or-public"></a><span id="Using_SymChk_to_determine_whether_symbols_are_private_or_public"></span><span id="using_symchk_to_determine_whether_symbols_are_private_or_public"></span><span id="USING_SYMCHK_TO_DETERMINE_WHETHER_SYMBOLS_ARE_PRIVATE_OR_PUBLIC"></span>使用 SymChk 以确定符号是否为专用或公用

若要确定是否专用或公共符号文件，请使用 **/v**参数使该 SymChk 显示详细输出。 假设 MyApp.exe 和 MyApp.pdb 位于文件夹 c:\\sym. 输入此命令。

```console
symchk /v c:\\sym\\MyApp.exe /s c:\\sym**
```

如果 MyApp.pdb 包含私有符号，SymChk 的输出如下所示。

```console
[SYMCHK] Searching for symbols to c:\sym\MyApp.exe in path c:\sym
...
DBGHELP: MyApp - private symbols & lines
        c:\sym\MyApp.pdb
...
SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

如果 MyApp.pdb 包含仅公共符号，SymChk 的输出如下所示。

```console
[SYMCHK] Searching for symbols to c:\sym\MyApp.exe in path c:\sym
...
DBGHELP: MyApp - public symbols
        c:\sym\MyApp.pdb
...
SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

若要限制您的搜索，以便查找仅公共符号文件，请使用**s**选项与 **/s**参数 (**/ss**)。 以下命令找到的匹配项，如果 MyApp.pdb 包含仅公共符号。 如果 MyApp.pdb 包含私有符号没有找到匹配项。

```console
symchk /v c:\\sym\\MyApp.exe /ss c:\\sym
```

有关详细信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面是一些示例。 以下命令搜索程序 Myapp.exe 的符号：

```console
e:\debuggers> symchk f:\myapp.exe /s f:\symbols\applications 

SYMCHK: Myapp.exe           FAILED  - Myapp.pdb is missing

SYMCHK: FAILED files = 1
SYMCHK: PASSED + IGNORED files = 0
```

你可以再次尝试使用不同的符号路径：

```console
e:\debuggers> symchk f:\myapp.exe /s f:\symbols\newdirectory 

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

搜索已成功这一次。 如果未使用详细选项，SymChk 将仅列出它无法找到符号文件。 因此在此示例中所不列出任何文件。 您可以告知搜索成功，因为现在是一个文件中的"传递"类别和无"失败"类别中列出。

如果它不包含任何可执行代码，则忽略程序文件。 此类型的多个资源文件。

如果想要查看所有的程序文件的文件名，则可以使用 **/v**选项以生成详细输出：

```console
e:\debuggers> symchk /v f:\myapp.exe /s f:\symbols\newdirectory 

SYMCHK: MyApp.exe           PASSED

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

以下命令会搜索 Windows 符号在符号服务器采用很多。 有多种可能的错误消息：

```console
e:\debuggers> symchk /r c:\windows\system32 /s srv*\\manysymbols\windows 

SYMCHK: msisam11.dll         FAILED  - MSISAM11.pdb is missing
SYMCHK: msuni11.dll          FAILED  - msuni11link.pdb is missing
SYMCHK: msdxm.ocx            FAILED  - Image is split correctly, but msdxm.dbg i
s missing
SYMCHK: expsrv.dll           FAILED  - Checksum doesn't match with expsrv.DBG
SYMCHK: imeshare.dll         FAILED  - imeshare.opt.pdb is missing
SYMCHK: ir32_32.dll          FAILED  - Built with no debugging information
SYMCHK: author.dll           FAILED  - rpctest.pdb is missing
SYMCHK: msvcrt40.dll         FAILED  - Built with no debugging information
......
SYMCHK: FAILED files = 211
SYMCHK: PASSED + IGNORED files = 4809
```

## <a name="see-also"></a>请参阅

[SymChk 命令行选项](symchk-command-line-options.md)

[使用符号服务器和符号存储区](symbol-stores-and-symbol-servers.md)


 





