---
title: 公共和专用符号
description: 公共和专用符号
keywords:
- 符号，公共
- 符号，专用
- 公共符号
- 私有符号
- 零售符号
- 导出符号
- 符号文件，完整符号文件
- 符号文件，去除符号文件
- 完整符号文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e79a689272a052210923b13b00dd50cb692aef8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811203"
---
# <a name="public-and-private-symbols"></a>公共和专用符号


当完整大小的 .pdb 或 dbg 符号文件由链接器生成时，它包含两个不同的信息集合： *私有符号数据* 和 *公共符号表*。 这些集合在它们所包含的项列表和它们存储的有关每个项的信息之间有所不同。

私有符号数据包括以下项：

-   函数

-   全局变量

-   局部变量

-   有关用户定义的结构、类和数据类型的信息

-   源文件的名称和该文件中对应于每个二进制指令的行号

公共符号表包含较少的项：

-   函数 (声明为 **静态** 的函数除外) 

-   指定为 **extern** (的全局变量和在多个对象文件中可见的任何其他全局变量) 

作为一般规则，公共符号表完全包含可从一个源文件访问另一个源文件的那些项。 仅在一个对象文件中可见的项（例如 **静态** 函数、仅在单个源文件内全局的变量和局部变量）不包含在公共符号表中。

这两个数据集合在每个项的信息中也有所不同。 对于私有符号数据中包含的每个项，通常会包含以下信息：

-   项的名称

-   虚拟内存中项的地址

-   帧指针省略每个函数 (FPO) 记录

-   每个变量、结构和函数的数据类型

-   每个函数的参数的类型和名称

-   每个局部变量的范围

-   与每个源文件中的每行关联的符号

另一方面，公共符号表仅存储有关其中包含的每个项的下列信息：

-   项的名称。

-   其模块的虚拟内存空间中的项的地址。 对于函数，这是它的入口点地址。

-   帧指针省略每个函数 (FPO) 记录。

换句话说，可以通过两种方式将公共符号数据视为私有符号数据的一个子集：它包含较短的项列表，还包含有关每个项的更少信息。 例如，公共符号数据根本不包含局部变量。 每个局部变量只包含在私有符号数据中，其地址、数据类型和作用域。 另一方面，函数同时包含在私有符号数据和公共符号表中，但当私有符号数据包括函数名、地址、FPO 记录、输入参数名称和类型以及输出类型时，公共符号表只包括函数名称、地址和 FPO 记录。

私有符号数据和公共符号表之间还有一个不同之处。 公共符号表中的许多项的名称都是使用前缀、后缀或两者 *修饰* 的名称。 这些修饰由 C 编译器、c + + 编译器和 MASM 组装器添加。 典型前缀包括一系列下划线或字符串 **\_ \_ imp \_** (指定导入的函数) 。 典型后缀包含一个或多个 at 符号 ( **@** ) 后跟地址或其他标识字符串。 链接器使用这些装饰器来区分符号，因为函数名称或全局变量名称可能会在不同的模块之间重复出现。 这些修饰是一般规则的一个例外，公共符号表是私有符号数据的一个子集。

### <a name="span-idfull_symbol_files_and_stripped_symbol_filesspanspan-idfull_symbol_files_and_stripped_symbol_filesspanfull-symbol-files-and-stripped-symbol-files"></a><span id="full_symbol_files_and_stripped_symbol_files"></span><span id="FULL_SYMBOL_FILES_AND_STRIPPED_SYMBOL_FILES"></span>完整符号文件和去除符号文件

*完整的符号文件* 同时包含 private 符号数据和公共符号表。 这种类型的文件有时称为 *private 符号文件*，但此名称具有误导性，这种文件包含私有和公共符号。

*去除符号文件* 是只包含公共符号表的较小文件，在某些情况下，它只包含公共符号表的子集。 此文件有时称为 *公共符号文件*。

### <a name="span-idcreating_full_and_stripped_symbol_filesspanspan-idcreating_full_and_stripped_symbol_filesspancreating-full-and-stripped-symbol-files"></a><span id="creating_full_and_stripped_symbol_files"></span><span id="CREATING_FULL_AND_STRIPPED_SYMBOL_FILES"></span>创建完整和去除符号文件

如果通过 Visual Studio 生成二进制文件，则可以创建完整或去除的符号文件。 生成二进制文件的 "调试版本" 时，Visual Studio 通常会创建完整的符号文件。 生成 "零售版" 时，Visual Studio 通常不创建任何符号文件，但如果设置了正确的选项，则将创建完整或去除的符号文件。

如果用生成实用工具生成二进制文件，实用工具将创建完整的符号文件。

使用 BinPlace 工具，可以从完整的符号文件创建一个去除的符号文件。 如果使用最常见的 BinPlace 选项 (**--x-n**) ，则会将去除的符号文件放置在 **-s** 开关之后列出的目录中，并将完整的符号文件放在 **-n** 开关之后列出的目录中。 当 BinPlace 去除某个符号文件时，会为该文件的去除文件和完整版本提供相同的签名和其他标识信息。 这允许你使用任一版本进行调试。

使用 Pdbcopy.exe 工具，可以通过删除私有符号数据从完整的符号文件创建一个去除的符号文件。 Pdbcopy.exe 还可以删除公共符号表的指定子集。 有关详细信息，请参阅 [pdbcopy.exe](pdbcopy.md)。

使用 SymChk 工具，可以确定符号文件是否包含私有符号。 有关详细信息，请参阅 [SymChk](symchk.md)。

### <a name="span-idviewing_public_and_private_symbols_in_the_debuggerspanspan-idviewing_public_and_private_symbols_in_the_debuggerspanviewing-public-and-private-symbols-in-the-debugger"></a><span id="viewing_public_and_private_symbols_in_the_debugger"></span><span id="VIEWING_PUBLIC_AND_PRIVATE_SYMBOLS_IN_THE_DEBUGGER"></span>查看调试器中的公共和私有符号

可以使用 WinDbg、KD 或 CDB 来查看符号。 当这些调试器中的一个具有访问完整符号文件的权限时，它将包含在私有符号数据中列出的信息以及公共符号表中列出的信息。 私有符号数据更详细，而公共符号数据包含符号修饰。

访问私有符号时，始终使用私有符号数据，因为公共符号表中不包含这些符号。 从不修饰这些符号。

访问公共符号时，调试器的行为取决于某些 [符号选项](symbol-options.md)：

-   当 [SYMOPT \_ UNDNAME](symbol-options.md#symopt-undname) 选项为 on 时，当显示公共符号的名称时，将不包括修饰。 而且，在搜索符号时，将忽略修饰。 如果此选项为 off，则在显示公共符号时显示修饰，在搜索中使用修饰。 在任何情况下，都不会修饰私有符号。 默认情况下，在所有调试器中启用此选项。

-   当 [SYMOPT \_ \_ 仅 PUBLICS](symbol-options.md#symopt-publics-only) 选项为 on 时，将忽略 private 符号数据，并且仅使用公共符号表。 默认情况下，此选项在所有调试器中处于关闭状态。

-   当 [SYMOPT \_ NO \_ PUBLICS](symbol-options.md#symopt-no-publics) 选项为 on 时，将忽略公共符号表，并且搜索和符号信息单独使用私有符号数据。 默认情况下，此选项在所有调试器中处于关闭状态。

-   当 [SYMOPT \_ AUTO \_ PUBLICS](symbol-options.md#symopt-auto-publics) 选项 (，且仅 SYMOPT \_ PUBLICS \_ 和 SYMOPT \_ NO \_ PUBLICS 都不) 时，将在私有符号数据中执行第一个符号搜索。 如果在此处找到所需的符号，则搜索将终止。 否则，会搜索公共符号表。 由于公共符号表包含专用数据中的符号子集，因此这通常会导致忽略公共符号表。

-   如果仅 SYMOPT \_ PUBLICS \_ 、SYMOPT \_ NO \_ PUBLICS 和 SYMOPT \_ AUTO \_ PUBLICS 选项均为 off，则每次需要符号时都会搜索私有符号数据和公共符号表。 但是，如果在这两个位置都找到匹配项，则使用私有符号数据中的匹配项。 因此，此实例中的行为与 SYMOPT \_ auto PUBLICS 为 on 时的行为相同 \_ ，不同之处在于使用 SYMOPT \_ 自动 \_ PUBLICS 可能导致符号搜索稍微快一些。

下面是一个示例，其中，命令 [**x (检查符号)**](x--examine-symbols-.md) 使用三次。 第一次使用默认的符号选项，因此，信息是从私有符号数据中获取的。 请注意，这包括有关数组 **typingString** 的地址、大小和数据类型的信息。 接下来，使用 symopt + 4000，使调试器忽略私有符号数据。 然后再次运行 **x** 命令时，将使用公共符号表;此时， **typingString** 没有大小和数据类型信息。 最后，使用 symopt-2，这会使调试器包含修饰。 在最后一次运行 **x** 命令时，将显示函数名 **\_ typingString** 的修饰版本。

```dbgcmd
0:000> x /t /d *!*typingstring* 
00434420 char [128] TimeTest!typingString = char [128] ""

0:000> .symopt+ 4000

0:000> x /t /d *!*typingstring* 
00434420 <NoType> TimeTest!typingString = <no type information>

0:000> .symopt- 2

0:000> x /t /d *!*typingstring* 
00434420 <NoType> TimeTest!_typingString = <no type information> 
```

### <a name="span-idviewing_public_and_private_symbols_with_the_dbh_toolspanspan-idviewing_public_and_private_symbols_with_the_dbh_toolspanviewing-public-and-private-symbols-with-the-dbh-tool"></a><span id="viewing_public_and_private_symbols_with_the_dbh_tool"></span><span id="VIEWING_PUBLIC_AND_PRIVATE_SYMBOLS_WITH_THE_DBH_TOOL"></span>通过 THIS->DBH 工具查看公共和私有符号

查看符号的另一种方法是使用 [this->dbh 工具](dbh.md)。 THIS->DBH 使用与调试器相同的符号选项。 与调试器类似，THIS->DBH [ \_ \_ 仅保留 SYMOPT PUBLICS](symbol-options.md#symopt-publics-only) ，默认情况下， [SYMOPT 不会关闭 \_ \_ PUBLICS](symbol-options.md#symopt-no-publics) ，并且默认情况下，将 [SYMOPT \_ UNDNAME](symbol-options.md#symopt-undname) 和 [SYMOPT \_ 自动 \_ PUBLICS](symbol-options.md#symopt-auto-publics) 打开。 可以通过命令行选项或 THIS->DBH 命令重写这些默认值。

下面是一个示例，其中使用了 THIS->DBH 命令 **addr 414fe0** 三次。 第一次使用默认的符号选项，因此，信息是从私有符号数据中获取的。 请注意，这包括有关函数 **fgets** 的地址、大小和数据类型的信息。 接下来，使用命令 symopt + 4000，这将导致 THIS->DBH 忽略私有符号数据。 当 **地址 414fe0** 再次运行时，将使用公共符号表;这一次没有函数 **fgets** 的大小和数据类型信息。 最后，使用命令 symopt-2，这将导致 THIS->DBH 包含修饰。 在最后一次运行 **地址 414fe0** 时，将显示函数名称 **\_ fgets** 的修饰版本。

```dbgcmd
pid:4308 mod:TimeTest[400000]: addr 414fe0

fgets
   name : fgets
   addr :   414fe0
   size : 113
  flags : 0
   type : 7e
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 7d

pid:4308 mod:TimeTest[400000]: symopt +4000

Symbol Options: 0x10c13
Symbol Options: 0x14c13

pid:4308 mod:TimeTest[400000]: addr 414fe0

fgets
   name : fgets
   addr :   414fe0
   size : 0
  flags : 0
   type : 0
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagPublicSymbol (a)
  index : 7f

pid:4308 mod:TimeTest[400000]: symopt -2

Symbol Options: 0x14c13
Symbol Options: 0x14c11

pid:4308 mod:TimeTest[400000]: addr 414fe0

_fgets
   name : _fgets
   addr :   414fe0
   size : 0
  flags : 0
   type : 0
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagPublicSymbol (a)
  index : 7f 
```

 

 





