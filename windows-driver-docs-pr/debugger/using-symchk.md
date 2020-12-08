---
title: 使用 SymChk
description: 使用 SymChk
keywords:
- SymChk，使用
ms.date: 10/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: c53b0281ac94a686986ecf97feb88eecf1f39c5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803061"
---
# <a name="using-symchk"></a>使用 SymChk


## <span id="ddk_using_symchk_dtoolq"></span><span id="DDK_USING_SYMCHK_DTOOLQ"></span>

SymChk 的基本语法如下所示：

```console
symchk [/r] FileNames /s SymbolPath 
```

*文件名* 指定需要其符号的一个或多个程序文件。 如果 *文件名* 为目录，并使用 **/r** 标志，则会以递归方式浏览该目录，SymChk 将尝试在此目录树中查找所有程序文件的符号。 *SymbolPath* 指定 SymChk 搜索符号的位置。

还有更多命令行选项。 有关完整列表，请参阅 [SymChk Command-Line 选项](symchk-command-line-options.md)。

### <a name="obtaining-symchk"></a>获取 symchk

与其他调试工具一样，Symchk 作为调试器的一部分提供。 有关详细信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。

安装调试工具后，symchk 在此目录中适用于64位 Windows。

C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64

### <a name="example-usage"></a>示例用法

指定的符号路径可以包含任意数量的本地目录、UNC 目录或符号服务器。 不以递归方式搜索本地目录和 UNC 目录。 仅搜索指定的目录和基于可执行文件扩展名的子目录。 例如，查询

```console
symchk thisdriver.sys /s g:\symbols 
```

将搜索 g： \\ mysymbols 和 g： \\ mysymbols \\ sys。


您可以使用以下语法之一来指定符号服务器，作为符号路径的一部分：

```console
srv*DownstreamStore*\\Server\Share
srv*\\Server\Share
```

这与在调试器的符号路径中使用符号服务器非常类似。 有关此内容的详细信息，请参阅 [使用符号服务器和符号存储](symbol-stores-and-symbol-servers.md)。

如果指定了下游存储，则 SymChk 将创建由符号服务器找到的所有有效符号文件的副本，并将这些文件放在下游存储中。 仅向下游复制完全匹配的符号文件。

在查询符号服务器之前，SymChk 始终搜索下游存储。 因此，当其他人维护符号存储区时，应谨慎使用下游存储。 如果你运行 SymChk 一次并找到符号文件，则会将这些文件复制到下游存储。 如果随后在符号存储区中更改或删除这些文件后再次运行 SymChk，则 SymChk 将不会注意到这种情况，因为它会在下游存储中找到要查找的内容，而无需进一步查看。

**注意**   SymChk 始终使用 SymSrv ( # A0) 作为其符号服务器 DLL。 另一方面，如果可用，则调试器可以选择除 SymSrv 之外的符号服务器 DLL。  (SymSrv 是 "用于 Windows 的调试工具" 包中包含的符号服务器 ) 
 

### <a name="span-idusing_symchk_to_determine_whether_symbols_are_private_or_publicspanspan-idusing_symchk_to_determine_whether_symbols_are_private_or_publicspanspan-idusing_symchk_to_determine_whether_symbols_are_private_or_publicspanusing-symchk-to-determine-whether-symbols-are-private-or-public"></a><span id="Using_SymChk_to_determine_whether_symbols_are_private_or_public"></span><span id="using_symchk_to_determine_whether_symbols_are_private_or_public"></span><span id="USING_SYMCHK_TO_DETERMINE_WHETHER_SYMBOLS_ARE_PRIVATE_OR_PUBLIC"></span>使用 SymChk 确定符号是私有的还是公共的

若要确定某个符号文件是私有的还是公共的，请使用 **/v** 参数，使 SymChk 显示详细输出。 假设 MyApp.exe 和 MyApp 位于文件夹 c： \\ 符号中。 输入此命令：

```console
symchk /v c:\\sym\\MyApp.exe /s c:\\sym**
```

如果 MyApp 包含 private 符号，则 SymChk 的输出将如下所示。

```console
[SYMCHK] Searching for symbols to c:\sym\MyApp.exe in path c:\sym
...
DBGHELP: MyApp - private symbols & lines
        c:\sym\MyApp.pdb
...
SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

如果 MyApp 只包含公共符号，则 SymChk 的输出将如下所示。

```console
[SYMCHK] Searching for symbols to c:\sym\MyApp.exe in path c:\sym
...
DBGHELP: MyApp - public symbols
        c:\sym\MyApp.pdb
...
SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

若要限制搜索以便仅查找公共符号文件，请使用带有 **/s** 参数的 **s** 选项 (**/ss**) 。 如果 MyApp 只包含公共符号，则以下命令将查找匹配项。 如果 MyApp 包含私有符号，则找不到匹配项。

```console
symchk /v c:\\sym\\MyApp.exe /ss c:\\sym
```

有关详细信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面是一些示例。 以下命令将搜索程序 Myapp.exe 的符号：

```console
e:\debuggers> symchk f:\myapp.exe /s f:\symbols\applications 

SYMCHK: Myapp.exe           FAILED  - Myapp.pdb is missing

SYMCHK: FAILED files = 1
SYMCHK: PASSED + IGNORED files = 0
```

你可以使用其他符号路径重试：

```console
e:\debuggers> symchk f:\myapp.exe /s f:\symbols\newdirectory 

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

此时间搜索成功。 如果未使用 verbose 选项，则 SymChk 将仅列出未能找到符号的文件。 因此，在此示例中未列出任何文件。 您可以判断搜索已成功，因为现在 "通过" 类别中列出了一个文件，而 "失败" 类别中没有任何文件。

如果程序文件不包含可执行代码，则会将其忽略。 这种类型的资源文件很多。

如果希望查看所有程序文件的文件名，可以使用 **/v** 选项生成详细输出：

```console
e:\debuggers> symchk /v f:\myapp.exe /s f:\symbols\newdirectory 

SYMCHK: MyApp.exe           PASSED

SYMCHK: FAILED files = 0
SYMCHK: PASSED + IGNORED files = 1
```

以下命令搜索符号服务器中的大量 Windows 符号。 有很多可能的错误消息：

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

## <a name="see-also"></a>另请参阅

[SymChk 命令行选项](symchk-command-line-options.md)

[使用符号服务器和符号存储区](symbol-stores-and-symbol-servers.md)


 





