---
title: 公共和专用符号
description: 公共和专用符号
ms.assetid: 61ed583d-8b97-4929-8d86-1a6353c13304
keywords:
- 公共符号
- 符号专用
- 公共符号
- 私有符号
- 零售符号
- 导出符号
- 符号文件，完整符号文件
- 符号文件，去除的符号文件
- 完整的符号文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac67a9dad14bc4d34712c74c29861144592aff8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576703"
---
# <a name="public-and-private-symbols"></a>公共和专用符号


链接器生成的全尺寸.pdb 或.dbg 符号文件后，它包含两个不同集合的信息：*私有符号数据*和一个*公共符号表*。 这些集合的区别在于它们所包含的项和存储有关每个项的信息的列表。

私有符号数据包括以下各项：

-   函数

-   全局变量

-   本地变量

-   有关用户定义的结构、 类和数据类型的信息

-   源文件和在该文件中每个二进制指令相对应的行号的名称

公共符号表包含较少的项：

-   函数 (声明的函数除外**静态**)

-   指定为全局变量**extern** （和任何其他全局变量可见跨多个对象文件）

作为一般规则，公共符号表包含完全到另一个源文件从可访问这些项。 只能在一个可见项的对象文件--例如**静态**函数、 变量仅在单个源文件，全局和本地变量-不包含公共符号表中。

这两个集合的数据也存在差异包括每个项中的信息。 将私有符号数据中包含的每个项通常包含以下信息：

-   项的名称

-   虚拟内存中的项的地址

-   每个函数的帧指针省略 (FPO) 记录

-   数据类型的每个变量、 结构和函数

-   类型和每个函数的参数的名称

-   每个本地变量的作用域

-   与每个源文件中的每行关联的符号

但是，公共符号表将存储仅包括在其中每个项有关的以下信息：

-   项的名称。

-   其模块的虚拟内存空间中的项的地址。 对于函数，这是其入口点的地址。

-   每个函数的帧指针省略 (FPO) 记录。

换而言之，公共符号数据可以认为的两种方式中的私有符号数据的子集： 它包含一个较短列表的项，并且它也包含有关每个项更少信息。 例如，公共符号数据不完全包括本地变量。 每个本地变量包含仅在私有符号数据中，使用其地址、 数据类型和作用域。 函数，但是，将包含私有符号数据和公共符号表中，但私有符号数据包括函数名称、 地址、 FPO 记录、 输入的参数名称和类型和输出类型，包括公共符号表只是函数名称、 地址和 FPO 记录。

没有私有符号数据和公共符号表之间的另一个差异。 许多公共符号表中的项具有的名称*修饰*与前缀、 后缀，或两者。 C 编译器、 c + + 编译器和 MASM 组装器会添加这些修饰。 典型的前缀包含下划线或字符串的一系列**\_ \_imp\_** （指定导入的函数）。 典型的后缀包含一个或多个 at 符号 ( **@** ) 后接地址或其他标识字符串。 链接器使用这些修饰来消除歧义符号，因为很可能是该函数名称或全局变量名无法重复多个不同的模块。 这些修饰是公共符号表是专用的符号数据的子集的一般规则的例外。

### <a name="span-idfullsymbolfilesandstrippedsymbolfilesspanspan-idfullsymbolfilesandstrippedsymbolfilesspanfull-symbol-files-and-stripped-symbol-files"></a><span id="full_symbol_files_and_stripped_symbol_files"></span><span id="FULL_SYMBOL_FILES_AND_STRIPPED_SYMBOL_FILES"></span>完整的符号文件和去除的符号文件

一个*完整符号文件*包含私有符号数据和公共符号表。 这种文件有时称为*私有符号文件*，但此名称是具有误导性，此类文件包含专用和公共符号。

一个*符号文件中去除*是只包含公共符号表的较小的文件或在某些情况下，只有公共符号表的子集。 此文件有时称为*公共符号文件*。

### <a name="span-idcreatingfullandstrippedsymbolfilesspanspan-idcreatingfullandstrippedsymbolfilesspancreating-full-and-stripped-symbol-files"></a><span id="creating_full_and_stripped_symbol_files"></span><span id="CREATING_FULL_AND_STRIPPED_SYMBOL_FILES"></span>创建完整和去除符号文件

如果您使用 Visual Studio 的二进制文件生成时，可以创建任一完整或去除符号文件。 在生成时二进制文件的"调试版本"，Visual Studio 通常会创建完整符号文件。 当构建"零售版本"，Visual Studio 通常创建没有符号文件，但完整或去除设置了适当的选项会创建符号文件。

如果生成二进制文件的位置与生成实用工具，它将创建完整的符号文件。

使用 BinPlace 工具，可以从完整符号文件创建去除的符号文件。 使用最常用的 BinPlace 选项时 (**-a-x-s-n**)，去除的符号文件后列出的目录中放置 **-s**开关，并且完整的符号文件放在目录中列出后 **-n**切换。 当 BinPlace 去除的符号文件时，去除和完整版本的文件有完全相同的签名和其他标识信息。 这可以使用任一版本进行调试。

使用 PDBCopy 工具，您可以创建去除的符号文件从完整符号文件通过删除私有符号数据。 PDBCopy 还可以删除指定的公共符号表的子集。 有关详细信息，请参阅[PDBCopy](pdbcopy.md)。

使用 SymChk 工具，可以确定的符号文件是否包含私有符号。 有关详细信息，请参阅[SymChk](symchk.md)。

### <a name="span-idviewingpublicandprivatesymbolsinthedebuggerspanspan-idviewingpublicandprivatesymbolsinthedebuggerspanviewing-public-and-private-symbols-in-the-debugger"></a><span id="viewing_public_and_private_symbols_in_the_debugger"></span><span id="VIEWING_PUBLIC_AND_PRIVATE_SYMBOLS_IN_THE_DEBUGGER"></span>查看调试器中的公共和私有符号

可以使用 WinDbg、 KD 或 CDB 来查看的符号。 当以下这些调试器之一有权访问完整的符号文件时，它具有专用的符号数据中所列的信息和公共符号表中列出的信息。 更多详细的私有符号数据，而公共符号数据包含符号修饰。

访问私有符号时, 始终使用专用的符号数据是因为这些符号不包含公共符号表中。 这些符号永远不会进行修饰。

在访问公共符号时，调试器的行为取决于某些[符号选项](symbol-options.md):

-   当[SYMOPT\_UNDNAME](symbol-options.md#symopt-undname)选项设置为 on，显示的公共符号名称时，可能不会包含修饰。 此外，搜索的符号时，将忽略修饰。 关闭此选项后，显示公共符号时，会显示修饰和修饰在搜索中使用。 在任何情况下，永远不会进行修饰私有符号。 此选项是在默认情况下，所有调试器中。

-   当[SYMOPT\_PUBLICS\_仅](symbol-options.md#symopt-publics-only)选项设置为 on，私有符号数据将被忽略，且使用仅公共符号表。 默认情况下，在所有调试器情况下，此选项处于关闭状态。

-   当[SYMOPT\_否\_PUBLICS](symbol-options.md#symopt-no-publics)选项设置为 on，公共符号表将被忽略，并搜索和符号信息使用单独的专用符号数据。 默认情况下，在所有调试器情况下，此选项处于关闭状态。

-   当[SYMOPT\_自动\_PUBLICS](symbol-options.md#symopt-auto-publics)选项设置为 on (和这两个 SYMOPT\_PUBLICS\_仅和 SYMOPT\_否\_PUBLICS 处于关闭状态)，第一个符号私有符号数据中执行搜索。 如果在其中找到所需的符号，则搜索将终止。 如果没有，则搜索公共符号表。 由于公共符号表包含专用的数据中的符号的子集，通常这会导致公共符号表被忽略。

-   当 SYMOPT\_PUBLICS\_仅，SYMOPT\_否\_PUBLICS 和 SYMOPT\_自动\_PUBLICS 选项是所有关闭的每个搜索私有符号数据和公共符号表符号所需的时间。 但是，当在这两个位置中找到匹配项，将使用私有符号数据中的匹配项。 因此，在此实例中的行为等同于何时 SYMOPT\_自动\_PUBLICS 处于打开状态，只不过使用 SYMOPT\_自动\_PUBLICS 可能会导致符号搜索发生这种情况会稍微快一些。

下面是在其中一个示例命令[ **（检查符号） x** ](x--examine-symbols-.md)使用三次。 第一次，使用默认符号选项，并因此信息来自私有符号数据。 请注意，这包括有关数组的地址、 大小和数据类型的信息**typingString**。 接下来，命令.symopt + 4000 使用，从而导致调试器忽略私有符号数据。 当**x**命令，然后再次运行，请使用公共符号表; 这一次没有任何大小和数据类型信息**typingString**。 最后，使用命令.symopt 2，这将导致调试器包括修饰。 当**x**命令将运行此最后一次，函数名称的修饰版本 **\_typingString**，所示。

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

### <a name="span-idviewingpublicandprivatesymbolswiththedbhtoolspanspan-idviewingpublicandprivatesymbolswiththedbhtoolspanviewing-public-and-private-symbols-with-the-dbh-tool"></a><span id="viewing_public_and_private_symbols_with_the_dbh_tool"></span><span id="VIEWING_PUBLIC_AND_PRIVATE_SYMBOLS_WITH_THE_DBH_TOOL"></span>查看公共和私有符号使用 DBH 工具

若要查看的符号的另一种方法是使用[DBH 工具](dbh.md)。 DBH 使用相同的符号选项作为调试器。 调试程序，如 DBH 离开[SYMOPT\_PUBLICS\_仅](symbol-options.md#symopt-publics-only)并[SYMOPT\_否\_PUBLICS](symbol-options.md#symopt-no-publics)是关闭的默认值，并关闭[SYMOPT\_UNDNAME](symbol-options.md#symopt-undname)并[SYMOPT\_自动\_PUBLICS](symbol-options.md#symopt-auto-publics)在默认情况下。 通过命令行选项或通过 DBH 命令，可以重写这些默认值。

下面是在其中一个示例 DBH 命令**addr 414fe0**使用三次。 第一次，使用默认符号选项，并因此信息来自私有符号数据。 请注意，这包含有关该函数的地址、 大小和数据类型的信息**fgets**。 接下来，使用命令 symopt +4000，这将导致 DBH 忽略私有符号数据。 当**addr 414fe0**然后再次运行，公共使用符号表; 这一次没有函数的大小和数据类型信息**fgets**。 最后，使用命令 symopt-2，这将导致 DBH 包括修饰。 当**addr 414fe0**是运行此最后一次，函数名称的修饰版本 **\_fgets**，所示。

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

 

 





