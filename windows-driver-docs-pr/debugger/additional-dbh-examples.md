---
title: 其他 DBH 示例
description: 其他 DBH 示例
keywords:
- THIS->DBH，显示符号
- THIS->DBH，符号修饰
- THIS->DBH，数据类型
- THIS->DBH，虚部
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4352df95f43cac14b8f0e856598a85031ce9338
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793305"
---
# <a name="additional-dbh-examples"></a>其他 DBH 示例


下面是可以在 THIS->DBH 提示符处发出的其他命令示例。

### <a name="span-iddisplaying_private_symbols_and_public_symbolsspanspan-iddisplaying_private_symbols_and_public_symbolsspandisplaying-private-symbols-and-public-symbols"></a><span id="displaying_private_symbols_and_public_symbols"></span><span id="DISPLAYING_PRIVATE_SYMBOLS_AND_PUBLIC_SYMBOLS"></span>显示私有符号和公共符号

如果目标是一个完整的符号文件，则每个公共符号在文件中出现两次：在公共符号表中，在私有符号数据中显示。 公共符号表中的副本通常包含)  (前缀和后缀的各种修饰。 有关详细信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

THIS->DBH 可以从私有符号数据、不含修饰的公共符号表以及带有修饰的公共符号表中显示此符号的相关信息。 下面是一个示例，其中全部三个都显示，每次使用 command **414fe0** 命令。

在此示例中，第一次出现此命令时，THIS->DBH 将使用默认的符号选项，因此生成的信息来自私有符号数据。 请注意，此信息包括函数 **fgets** 的地址、大小和数据类型。 然后，使用命令 symopt + 4000，这将打开 SYMOPT \_ PUBLICS \_ 选项。 这将导致 THIS->DBH 忽略私有符号数据，因此，当 **414fe0** 命令第二次运行时，this->dbh 使用公共符号表，并且不显示函数 **fgets** 的大小或数据类型信息。 最后，使用命令 symopt-2，关闭 SYMOPT \_ UNDNAME 选项，并使 this->dbh 包含修饰。 当 **地址 414fe0** 最后一次运行时，它会显示函数名称 **\_ fgets** 的修饰版本。

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

如果使用了-d 命令行选项，则结果将从开头开始显示修饰的公共名称。

### <a name="span-iddetermining_the_decorations_of_a_specific_symbolspanspan-iddetermining_the_decorations_of_a_specific_symbolspandetermining-the-decorations-of-a-specific-symbol"></a><span id="determining_the_decorations_of_a_specific_symbol"></span><span id="DETERMINING_THE_DECORATIONS_OF_A_SPECIFIC_SYMBOL"></span>确定特定符号的修饰

THIS->DBH 可以根据特定符号确定修饰。 当与需要使用其修饰（如 [pdbcopy.exe](pdbcopy.md)）指定符号的程序结合使用时，这可能很有用。

例如，假设您知道符号文件 mysymbols 包含其修饰名为 **MyFunction1** 的符号。 若要查找修饰名称，请使用以下过程。

首先，在不使用-d 命令行选项的情况下启动 THIS->DBH，然后使用 symopt + 4000 命令，以便所有信息都来自公共符号表：

```console
C:\> dbh c:\mydir\mysymbols.pdb

mysymbols [1000000]: symopt +4000

Symbol Options: 0x10c13
Symbol Options: 0x14c13 
```

接下来，使用 **name** 命令或 **enum** 命令显示所需符号的地址：

```dbgcmd
mysymbols [1000000]: enum myfunction1 

 index            address     name
   2ab            102cb4e :   MyFunction1
```

现在，使用 symopt 来使符号修饰可见，然后将 **addr** 命令与此符号的地址一起使用：

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

这会显示符号的修饰名为 **\_MyFunction1@4** 。

### <a name="span-iddecoding_symbol_decorationsspanspan-iddecoding_symbol_decorationsspandecoding-symbol-decorations"></a><span id="decoding_symbol_decorations"></span><span id="DECODING_SYMBOL_DECORATIONS"></span>解码符号修饰

**Undec** 命令可用于显示 c + + 符号修饰的含义。 在下面的示例中，将装饰附加到？？ \_C@ \_ 03GGCAPAJC@Sep ？ $AA @ 将进行解码，以指示它是一个字符串：

```dbgcmd
dbh: undec ??_C@_03GGCAPAJC@Sep?$AA@

??_C@_03GGCAPAJC@Sep?$AA@ =
`string' 
```

下面的示例对附加到三个函数名称的修饰进行解码，并显示它们的原型：

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

**Undec** 命令不显示有关初始下划线、前缀 **\_ \_ imp \_** 或尾部 " **@** <em>address</em>" 修饰的信息，这些信息通常会附加到函数名称。

可以将 **undec** 命令与任何字符串一起使用，而不只是在当前加载的模块中使用符号的名称。

### <a name="span-idsorting_a_list_of_symbols_by_addressspanspan-idsorting_a_list_of_symbols_by_addressspansorting-a-list-of-symbols-by-address"></a><span id="sorting_a_list_of_symbols_by_address"></span><span id="SORTING_A_LIST_OF_SYMBOLS_BY_ADDRESS"></span>按地址对符号列表进行排序

如果只是想要按地址顺序排序的符号列表，可以在批处理模式下运行 THIS->DBH，并通过管道将结果传递给 **sort** 命令。 地址值通常从每行的第18列开始，因此以下命令将按地址对结果进行排序：

```dbgcmd
dbh -p:4672 enum mymodule!* | sort /+18
```

### <a name="span-iddisplaying_source_line_informationspanspan-iddisplaying_source_line_informationspandisplaying-source-line-information"></a><span id="displaying_source_line_information"></span><span id="DISPLAYING_SOURCE_LINE_INFORMATION"></span>显示源行信息

使用完整符号文件时，THIS->DBH 可以显示源行信息。 这不需要访问任何源文件，因为此信息存储在符号文件本身中。

此处的 " **行** " 命令显示与指定的源行对应的二进制指令的十六进制地址，并显示与该行关联的符号。  (在此示例中，没有与此行关联的符号。 ) 

```dbgcmd
dbh [1000000]: line myprogram.cpp#767

   file : e:\mydirectory\src\myprogram.cpp
   line : 767
   addr :  1006191
    key : 0000000000000000
disp : 0
```

此处的 **srclines** 命令显示与指定的源行关联的对象文件：

```dbgcmd
dbh [1000000]: srclines myprogram.cpp 767

0x1006191: e:\mydirectory\objchk\amd64\myprogram.obj
line 767 e:\mydirectory\src\myprogram.cpp
```

请注意， **srclines** 的输出类似于 [**Ln (列出最接近)**](ln--list-nearest-symbols-.md) 调试器命令的符号。

### <a name="span-iddisplaying_a_data_typespanspan-iddisplaying_a_data_typespandisplaying-a-data-type"></a><span id="displaying_a_data_type"></span><span id="DISPLAYING_A_DATA_TYPE"></span>显示数据类型

**Type** 命令可用于显示有关数据类型的信息。 此处显示了有关 CMDPROC 类型的数据：

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

"Tag" 后列出的值指定了此数据类型的性质。 在这种情况下， **SymTagTypedef** 指示该类型是使用 **typedef** 语句定义的。

### <a name="span-idusing_imaginary_symbolsspanspan-idusing_imaginary_symbolsspanusing-imaginary-symbols"></a><span id="using_imaginary_symbols"></span><span id="USING_IMAGINARY_SYMBOLS"></span>使用虚符号

" **添加** " 命令可将一个虚符号添加到已加载的模块。 实际的符号文件未更改;只有 THIS->DBH 的内存中该文件的图像会发生更改。

如果希望暂时重写与给定的地址范围关联的符号，则 " **添加** " 命令会很有用。 在下面的示例中，与 **MyModule！ main** 关联的地址范围的一部分由虚部 **MyModule！幻** 数重写。

下面是在添加虚部符号之前模块的显示方式。 请注意， **main** 函数从0x0042CC56 开始，大小为0x42B。 因此，当将 **addr** 命令与地址0x0042CD10 一起使用时，它会将此地址识别为 **main** 函数边界内的内容：

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

现在，符号 **幻** 数添加到地址0x0042CD00，大小为0x10 个字节。 使用 **enum** 命令时，将设置索引中的高位，并显示这是一个虚符号：

```dbgcmd
pid:6040 mod:MyModule[400000]: add magic 42cd00 10


pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup
  80000001             42cd00 :   magic 
```

使用 address **命令时，将查找** 其范围包含指定地址的任何符号。 由于此搜索从指定地址开始，并向后运行，因此地址0x004CD10 现在与 **幻** 数关联。 另一方面，地址0x004CD40 仍与 **main** 关联，因为它位于 **幻** 符号的范围之外。 另请注意，标记 **SymTagCustom** 指示一个虚符号：

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

最后， **del** 命令可以删除符号 **幻**，并将所有符号返回到其原始范围：

```dbgcmd
pid:6040 mod:MyModule[400000]: del magic


pid:6040 mod:MyModule[400000]: enum timetest!ma*

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup 
```









