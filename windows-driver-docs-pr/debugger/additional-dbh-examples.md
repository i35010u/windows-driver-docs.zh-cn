---
title: 其他 DBH 示例
description: 其他 DBH 示例
ms.assetid: 6db23b6b-e5da-4ea3-9f0a-ab42c0e712d7
keywords:
- DBH，显示符号
- DBH，符号修饰
- DBH，数据类型
- DBH，虚部符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21292ca6ed92b9fc419dae7231298ca630ca6183
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354811"
---
# <a name="additional-dbh-examples"></a>其他 DBH 示例


以下是可以在 DBH 提示符处发出的命令的其他示例。

### <a name="span-iddisplayingprivatesymbolsandpublicsymbolsspanspan-iddisplayingprivatesymbolsandpublicsymbolsspandisplaying-private-symbols-and-public-symbols"></a><span id="displaying_private_symbols_and_public_symbols"></span><span id="DISPLAYING_PRIVATE_SYMBOLS_AND_PUBLIC_SYMBOLS"></span>显示私有符号和公共符号

如果目标是完整的符号文件，则每个公共符号将出现在文件中两次： 在公共符号表中，并在专用的符号数据中。 公共符号表中的副本通常包含各种修饰的文本 （前缀和后缀）。 有关详细信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

DBH 可以显示此符号从私有符号数据，不修饰，包含的公共符号表和具有修饰的公共符号表有关的信息。 下面是的示例中的所有这三个显示，使用命令**addr 414fe0**每次。

此命令将显示在此示例中，第一次 DBH 使用默认符号选项，因此生成的信息来自私有符号数据。 请注意，此信息包含该函数的地址、 大小和数据类型**fgets**。 然后，使用命令 symopt +4000，开启 SYMOPT\_PUBLICS\_仅选项。 这将导致 DBH 要忽略的私有符号数据，因此当**addr 414fe0**第二次运行命令，DBH 使用公共符号表中，并为该函数显示无大小或数据类型信息**fgets**. 最后，使用命令 symopt-2，关闭 SYMOPT\_UNDNAME 选项，它导致 DBH 包括修饰。 当**addr 414fe0**运行此最后一次，它会显示函数名称的修饰的版本 **\_fgets**。

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

如果已使用-d 的命令行选项，结果将显示从开始处的修饰公共名称。

### <a name="span-iddeterminingthedecorationsofaspecificsymbolspanspan-iddeterminingthedecorationsofaspecificsymbolspandetermining-the-decorations-of-a-specific-symbol"></a><span id="determining_the_decorations_of_a_specific_symbol"></span><span id="DETERMINING_THE_DECORATIONS_OF_A_SPECIFIC_SYMBOL"></span>确定特定符号的修饰

DBH 可以确定特定符号的修饰。 这可以是与要求要使用其修饰，如指定的符号的程序结合使用时很有用[PDBCopy](pdbcopy.md)。

例如，假设您知道，包含其未修饰的名是符号，符号文件 mysymbols.pdb **MyFunction1**。 若要查找的修饰的名，请使用以下过程。

首先，如果不使用-d 的命令行选项，启动 DBH，然后使用 symopt +4000 命令，以便所有信息都均来自公共符号表：

```console
C:\> dbh c:\mydir\mysymbols.pdb

mysymbols [1000000]: symopt +4000

Symbol Options: 0x10c13
Symbol Options: 0x14c13 
```

接下来，使用**名称**命令或**枚举**命令以显示所需的符号的地址：

```dbgcmd
mysymbols [1000000]: enum myfunction1 

 index            address     name
   2ab            102cb4e :   MyFunction1
```

现在使用 symopt-2 使符号修饰可见，然后再使用**addr**命令与此符号的地址：

```dbgcmd
mysymbols [1000000]: symopt -2

Symbol Options: 0x14c13
Symbol Options: 0x14c11

mysymbols [1000000]: addr 102cb4e

_MyFunction1@4
   name : _InterlockedIncrement@4
   addr :  102cb4e
   size : 0
  flags : 0
   type : 0
modbase :  1000000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagPublicSymbol (a)
  index : 2ab  
```

这会显示该符号的修饰的名是**\_ MyFunction1@4**。

### <a name="span-iddecodingsymboldecorationsspanspan-iddecodingsymboldecorationsspandecoding-symbol-decorations"></a><span id="decoding_symbol_decorations"></span><span id="DECODING_SYMBOL_DECORATIONS"></span>解码符号修饰

**Undec**命令可用于显示的含义C++符号修饰。 以下示例中，在装饰物附加到??\_C @\_03GGCAPAJC@Sep？ $AA @ 解码以指示它是一个字符串：

```dbgcmd
dbh: undec ??_C@_03GGCAPAJC@Sep?$AA@

??_C@_03GGCAPAJC@Sep?$AA@ =
`string' 
```

下面的示例解码附加到三个函数名称，显示其原型的修饰：

```dbgcmd
dbh: undec ?gcontext@@3_KA

?gcontext@@3_KA =
unsigned __int64 gcontext


dbh: undec ?pathcpy@@YGXPAGPBG1K@Z

?pathcpy@@YGXPAGPBG1K@Z =
void __stdcall pathcpy(unsigned short *,unsigned short const *,unsigned short const *,unsigned long)


dbh: undec ?_set_new_handler@@YAP6AHI@ZP6AHI@Z@Z

?_set_new_handler@@YAP6AHI@ZP6AHI@Z@Z =
int (__cdecl*__cdecl _set_new_handler(int (__cdecl*)(unsigned int)))(unsigned int) 
```

**Undec**命令不显示有关初始下划线，前缀信息 **\_ \_imp\_**，空格或尾随"**@**<em>地址</em>"效果，它们通常位于附加到函数名称。

可以使用**undec**命令与任何字符串，而不仅仅是当前加载的模块中的符号的名称。

### <a name="span-idsortingalistofsymbolsbyaddressspanspan-idsortingalistofsymbolsbyaddressspansorting-a-list-of-symbols-by-address"></a><span id="sorting_a_list_of_symbols_by_address"></span><span id="SORTING_A_LIST_OF_SYMBOLS_BY_ADDRESS"></span>按地址的符号列表进行排序

如果只是想符号，按地址顺序排序的列表可以运行 DBH 中批处理模式并通过管道将结果与**排序**命令。 地址值通常开始第 18 列中的每个行，因此，以下命令按地址对结果进行排序：

```dbgcmd
dbh -p:4672 enum mymodule!* | sort /+18
```

### <a name="span-iddisplayingsourcelineinformationspanspan-iddisplayingsourcelineinformationspandisplaying-source-line-information"></a><span id="displaying_source_line_information"></span><span id="DISPLAYING_SOURCE_LINE_INFORMATION"></span>显示源代码行信息

当您使用的完整符号文件时，DBH 可以显示源代码行信息。 由于此信息存储在符号文件本身，这不需要任何源文件的访问权限。

在这里，**行**命令将显示十六进制的二进制说明对应于指定的源行，而且它会显示与该行关联的符号。 （在此示例中，有与行相关的无符号。）

```dbgcmd
dbh [1000000]: line myprogram.cpp#767

   file : e:\mydirectory\src\myprogram.cpp
   line : 767
   addr :  1006191
    key : 0000000000000000
disp : 0
```

在这里， **srclines**命令将显示与指定的源行关联的对象文件：

```dbgcmd
dbh [1000000]: srclines myprogram.cpp 767

0x1006191: e:\mydirectory\objchk\amd64\myprogram.obj
line 767 e:\mydirectory\src\myprogram.cpp
```

请注意，输出**srclines**是类似于[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)调试器命令。

### <a name="span-iddisplayingadatatypespanspan-iddisplayingadatatypespandisplaying-a-data-type"></a><span id="displaying_a_data_type"></span><span id="DISPLAYING_A_DATA_TYPE"></span>显示的数据类型

**类型**命令可以用于显示有关数据类型的信息。 此处它会显示有关 CMDPROC 类型的数据：

```dbgcmd
dbh [1000000]: type CMDPROC

   name : CMDPROC
   addr :        0
   size : 8
  flags : 0
   type : c
modbase :  1000000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagTypedef (11)
  index : c
```

列出后"标记"指定此数据类型的特性的值。 在这种情况下， **SymTagTypedef**指示此类型已定义使用**typedef**语句。

### <a name="span-idusingimaginarysymbolsspanspan-idusingimaginarysymbolsspanusing-imaginary-symbols"></a><span id="using_imaginary_symbols"></span><span id="USING_IMAGINARY_SYMBOLS"></span>使用虚符号

**添加**命令可以将一个假想的符号添加到已加载模块。 实际的符号文件不会更改;更改只有在 DBH 的内存中该文件的映像。

**添加**命令可以是你想要暂时覆盖哪些符号是与给定的地址范围相关联的情况下很有用。 在以下示例中，与关联的地址范围的一部分**MyModule ！ 主要**虚部符号中被重写**MyModule ！ magic**。

下面是添加虚符号之前，该模块的显示方式。 请注意，**主要**函数开始 0x0042CC56，并且其大小 0x42B。 因此，在**addr**命令使用地址 0x0042CD10，它会将此地址识别为位于的边界内**主要**函数：

```dbgcmd
pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup

pid:6040 mod:MyModule[400000]: addr 42cc56

main
   name : main
   addr :   42cc56
   size : 42b
  flags : 0
   type : 2
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 1

pid:6040 mod:MyModule[400000]: addr 42cd10

main+ba
   name : main
   addr :   42cc56
   size : 42b
  flags : 0
   type : 2
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 1 
```

现在的符号**magic**大小 0x10 字节的地址 0x0042CD00，在添加。 当**枚举**使用命令，设置了高位索引中的，显示这一个假想的符号：

```dbgcmd
pid:6040 mod:MyModule[400000]: add magic 42cd00 10


pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup
  80000001             42cd00 :   magic 
```

当**addr**使用命令时，它会查找其范围包括指定的地址的任何符号。 由于此搜索与指定的地址和向后运行开始，现在与关联的地址 0x004CD10 **magic**。 另一方面，地址 0x004CD40 是依旧**主要**，因为它处于范围之外**magic**符号。 另请注意，标记**SymTagCustom**指示虚部符号：

```dbgcmd
pid:6040 mod:MyModule[400000]: addr 42cd10

magic+10
   name : magic
   addr :   42cd00
   size : 10
  flags : 1000
   type : 0
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagCustom (1a)
  index : 80000001

pid:6040 mod:MyModule[400000]: addr 42cd40

main+ea
   name : main
   addr :   42cc56
   size : 42b
  flags : 0
   type : 2
modbase :   400000
  value :        0
    reg : 0
  scope : SymTagNull (0)
    tag : SymTagFunction (5)
  index : 1 
```

最后， **del**命令可以删除符号**magic**，返回到其原始范围的所有符号：

```dbgcmd
pid:6040 mod:MyModule[400000]: del magic


pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup 
```









