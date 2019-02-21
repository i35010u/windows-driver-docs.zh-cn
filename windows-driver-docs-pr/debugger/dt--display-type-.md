---
title: dt （显示类型）
description: Dt 命令显示有关本地变量、 全局变量或数据类型的信息。 这可以显示关于简单数据类型，以及结构和联合的信息。
ms.assetid: 82aba13e-6604-46ca-b3e5-bb865ecf3f1f
keywords:
- dt （显示类型） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dt (Display Type)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5ee88b52ddfe5a3d843d7c82d89cf69afc795bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540762"
---
# <a name="dt-display-type"></a>dt （显示类型）


**Dt**命令显示有关本地变量、 全局变量或数据类型的信息。 这可以显示关于简单数据类型，以及结构和联合的信息。

用户模式语法

```dbgcmd
dt [-DisplayOpts] [-SearchOpts] [module!]Name [[-SearchOpts] Field] [Address] [-l List] 
dt [-DisplayOpts] Address [-l List] 
dt -h 
```

内核模式语法

```dbgcmd
[Processor] dt [-DisplayOpts] [-SearchOpts] [module!]Name [[-SearchOpts] Field] [Address] [-l List] 
dt [-DisplayOpts] Address [-l List] 
dt -h 
```

## <a name="span-idddkcmddisplaytypedbgspanspan-idddkcmddisplaytypedbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定包含所需的信息在进程运行的处理器。 有关详细信息，请参阅[包含多个处理器语法](multiprocessor-syntax.md)。 只能在内核模式下指定处理器。

<span id="_______DisplayOpts______"></span><span id="_______displayopts______"></span><span id="_______DISPLAYOPTS______"></span> *DisplayOpts*   
指定一个或多个以下表中给定的选项。 这些选项都以连字符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-a</strong>[<em>quantity</em>]</p></td>
<td align="left"><p>带有其索引的新行上显示每个数组元素。 总共<em>数量</em>将显示元素。 必须有之间没有空格并<em>quantity</em>。 如果<strong>-a</strong>后面不接数字，该数组中的所有项所都示。 <strong>-A</strong>[<em>quantity</em>] 开关应出现立即每个类型名称或字段名称的前您想在这种方式中显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong></p></td>
<td align="left"><p>显示基块以递归方式。 如果显示的结构包含子结构，它是以递归方式展开到任意深度和完整显示。 仅当它们是不在子结构的原始结构中，指针会展开。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>压缩输出。 如有可能在同一行显示所有字段。 (与一起使用时<strong>-a</strong>交换机，每个数组元素都占用一行，而不是格式为多个行块。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>与一起使用时<em>名称</em>的已结束，但一个星号，显示以开头的所有类型的详细输出<em>名称</em>。 如果<em>名称</em>不以星号结尾，则显示详细输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>强制<strong>dt</strong>枚举类型。 如果仅需要此选项<strong>dt</strong>错误地解释<em>名称</em>实例而不是一种类型的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-i</strong></p></td>
<td align="left"><p>不缩进子类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-o</strong></p></td>
<td align="left"><p>省略结构字段的偏移量的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-p</strong></p></td>
<td align="left"><p><em>地址</em>是一个物理地址，而不是虚拟的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-r</strong>[<em>depth</em>]</p></td>
<td align="left"><p>以递归方式转储的子类型字段。 如果<em>深度</em>是，此递归将停止后<em>深度</em>级别。 <em>深度</em>都必须是介于 1 和 9 之间的数字和必须之间没有空格<strong>r</strong>并<em>深度</em>。 <strong>-R</strong>[<em>深度</em>] 交换机应出现在立即之前地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong> <em>size</em></p></td>
<td align="left"><p>仅这些中的类型的大小字节数等于的值枚举<em>大小</em>。 <strong>-S</strong>正在枚举类型时，选项才有用。 当<strong>-s</strong>指定，则<strong>-e</strong>始终也暗示。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>枚举仅适用于类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>详细输出。 这样，例如总大小的结构和它的元素数的其他信息。 这用于时沿<strong>-y</strong>搜索选项，将显示所有符号，甚至包括那些没有关联的类型信息。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______SearchOpts______"></span><span id="_______searchopts______"></span><span id="_______SEARCHOPTS______"></span> *SearchOpts*   
指定一个或多个以下表中给定的选项。 这些选项都以连字符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-n</strong></p></td>
<td align="left"><p>这表示下一个参数是一个名称。 这应在下一项完全十六进制字符组成，因为它否则将执行作为一个地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-y</strong></p></td>
<td align="left"><p>这指示下一个参数的名称，不一定是整个名称开头。 当<strong>-y</strong>是包含，所有列出了匹配项，然后上列表中的第一个匹配项的详细信息。 如果<strong>-y</strong>是未包含，就会显示仅完全匹配项。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______module______"></span><span id="_______MODULE______"></span> *module*   
可选参数，指定定义此结构的模块。 如果没有本地变量或具有全局变量或类型的名称相同的类型，则应包含*模块*来指定是指全局变量。 否则为**dt**命令将显示本地变量，即使本地变量是不区分大小写的匹配项和全局变量是区分大小写的匹配项。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
指定类型或全局变量的名称。 如果*名称*有一个星号 (**\\* * *)，将显示所有匹配项的列表。因此， **dt A\\***  将列出所有数据类型、 全局函数和静态变量"A"开头，但将不会显示这些类型的实际实例。 (如果 **-v**在同一时间使用显示选项，将显示所有符号，而不仅仅是那些具有关联的类型信息。)也可以替换*名称*期 (**。**) 来表示你想要最新重复使用了值*名称*。

如果*名称*包含空格，它应括在括号中。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span> *字段*   
指定要显示的字段。 如果*字段*是省略，将显示所有字段。 如果*字段*跟一个句点 (**。**)，也将显示此字段的第一级子文件夹。 如果*字段*后接一系列的段，子字段会显示深度等于周期数。 跟一个句点任何字段名称将被视为前缀匹配项，如同 **-y**使用搜索选项。 如果*字段*后跟一个星号 (\*)，它将被视为字段中，不一定是整个字段开始并将显示所有匹配的字段。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的结构的地址。 如果*名称*省略，则*地址*必须包括，并且必须指定一个全局变量的地址。 *地址*用作虚拟地址，除非另行指定。 使用 **-p**选项来指定物理地址。 使用"at"符号 ( **@** ) 来指定寄存器 (例如， <strong>@eax</strong>)。

<span id="_______List______"></span><span id="_______list______"></span><span id="_______LIST______"></span> *列表*   
指定链接的链接的列表的字段名称。 *地址*参数必须包含。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

内存操作的概述和其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

**Dt**命令输出将始终在基数为 10，并以十六进制格式的无符号的数字中显示有符号的数字。

所有参数**dt**的允许的符号值还允许字符串使用通配符。 请参阅[字符串通配符语法](string-wildcard-syntax.md)有关详细信息。

**-Y**并 **-n**选项可以位于任何*名称*或者*字段*。 **-Y**选项允许您指定的类型或结构名称的开头。 例如， **dt y ALLEN**将显示有关类型的数据**ALLENTOWN**。 但是，您无法显示类型**ALLENTOWN**与**dt y A**。相反，您必须使用**dt-ny A**，因为**A**是有效的十六进制值，将被解释为地址，无需 **-n**选项。

如果*名称*指示一个结构，将显示所有字段 (例如， **dt myStruct**)。 如果只想一个特定字段，则可以执行**dt myStruct myField**。 这将显示调用 C 的成员**myStruct.myField**。 但请注意，该命令**dt myStruct myField1 myField2**显示**myStruct.myField1**并**myStruct.myField2**。 它不会显示**myStruct.myField1.myField2**。

如果结构名称或字段后跟下标，这将指定数组的单个实例。 例如， **dt myStruct myFieldArray\[3\]** 将显示有问题的数组的第四个元素。 但如果类型名称后跟下标，此参数指定整个数组。 例如， **dt CHAR\[8\] myPtr**将显示 8 个字符字符串。 下标总是采用为十进制而不考虑当前基数;**0x**前缀会导致错误。

由于该命令使用的类型信息。*pdb*文件，自由地可用于调试任何 CPU 平台。

使用的类型信息**dt**包括与创建的所有类型名称**typedef**，包括所有 Windows 定义的类型。 例如，**无符号长**并**char**不是有效的类型名称，但**ULONG**并**CHAR**是。 请参阅 Microsoft Windows SDK 的所有 Windows 的完整列表的类型名称。

创建的所有类型**typedef**中你自己的代码将会显示，只要它们实际已使用在程序中。 但是，在标头中定义但永远不会实际使用的类型不能.pdb 符号文件中存储并且将无法访问到调试器。 若要使这种类型可供调试器使用，将其用作*输入*的**typedef**语句。 例如，如果在代码中，结构 MY 显示以下\_数据将存储在.pdb 符号文件也可以显示**dt**命令：

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA;
typedef  MY_DATA *PMY_DATA; 
```

但是，下面的代码将无法满足需要因为这两个 MY\_数据和 PMY\_数据定义的初始**typedef** ，因此，MY\_数据本身尚未使用作为的输入任何**typedef**语句：

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA, *PMY_DATA; 
```

在任何情况下，只能在完整符号文件，而不是已去除私有符号的所有信息的符号文件中包括类型信息。 有关详细信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

如果你想要显示的 unicode 字符串，您必须使用[ **.enable\_（启用 Unicode 显示） 的 unicode** ](-enable-unicode--enable-unicode-display-.md)首先命令。 您可以控制长整数的显示[ **.enable\_长\_状态 （启用长整数显示）** ](-enable-long-status--enable-long-integer-display-.md)命令。

在以下示例中， **dt**显示全局变量：

```dbgcmd
0:000> dt mt1 
   +0x000 a                : 10
   +0x004 b                : 98 'b'
   +0x006 c                : 0xdd
   +0x008 d                : 0xabcd
   +0x00c gn               : [6] 0x1
   +0x024 ex               : 0x0 
```

在以下示例中， **dt**显示数组字段**gn**:

```dbgcmd
0:000> dt mt1 -a gn 
   +0x00c gn : 
    [00] 0x1
    [01] 0x2
    [02] 0x3
    [03] 0x4
    [04] 0x5
    [05] 0x6 
```

以下命令将显示变量的某些子字段：

```dbgcmd
0:000> dt mcl1 m_t1 dpo 
   +0x010 dpo  : DEEP_ONE
   +0x070 m_t1 : MYTYPE1 
```

下面的命令显示的字段的子字段**m\_t1**。 因为段会自动导致前缀匹配，这将显示子字段开头的任何字段的"m\_t1":

```dbgcmd
0:000> dt mcl1 m_t1. 
   +0x070 m_t1  : 
      +0x000 a     : 0
      +0x004 b     : 0 '
      +0x006 c     : 0x0
      +0x008 d     : 0x0
      +0x00c gn    : [6] 0x0
      +0x024 ex    : 0x0 
```

无法为任何深度重复此步骤。 例如，命令**dt mcl1...c。** 将显示所有字段深度四个，以便第一个字段名称开头和第三个字段名称开头**c**。

下面是可以显示子字段的方式的更详细的示例。 首先，显示**Ldr**字段：

```dbgcmd
0:000> dt nt!_PEB Ldr 7ffdf000 
   +0x00c Ldr : 0x00191ea0 
```

现在请展开指针类型字段：

```dbgcmd
0:000> dt nt!_PEB Ldr Ldr. 7ffdf000 
   +0x00c Ldr  : 0x00191ea0
      +0x000 Length : 0x28
      +0x004 Initialized : 0x1 '
      +0x008 SsHandle : (null)
      +0x00c InLoadOrderModuleList : _LIST_ENTRY [ 0x191ee0 - 0x192848 ]
      +0x014 InMemoryOrderModuleList : _LIST_ENTRY [ 0x191ee8 - 0x192850 ]
      +0x01c InInitializationOrderModuleList : _LIST_ENTRY [ 0x191f58 - 0x192858 ]
      +0x024 EntryInProgress : (null) 
```

现在，显示**CriticalSectionTimeout**字段：

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout 7ffdf000 
   +0x070 CriticalSectionTimeout : _LARGE_INTEGER 0xffffe86d`079b8000 
```

现在展开**CriticalSectionTimeout**结构子字段一个层次深度：

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout. 7ffdf000 
   +0x070 CriticalSectionTimeout  :  0xffffe86d`079b8000
      +0x000 LowPart                 : 0x79b8000
      +0x004 HighPart                : -6035
      +0x000 u                       : __unnamed
      +0x000 QuadPart                : -25920000000000 
```

现在展开**CriticalSectionTimeout**结构深度的子字段两个级别：

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout.. 7ffdf000 
   +0x070 CriticalSectionTimeout   :  0xffffe86d`079b8000
      +0x000 LowPart                  : 0x79b8000
      +0x004 HighPart                 : -6035
      +0x000 u                        :
         +0x000 LowPart                  : 0x79b8000
         +0x004 HighPart                 : -6035
      +0x000 QuadPart                 : -25920000000000 
```

下面的命令显示数据类型位于地址 0x0100297C MYTYPE1 的实例：

```dbgcmd
0:000> dt 0x0100297c MYTYPE1 
   +0x000 a                : 22
   +0x004 b                : 43 '+'
   +0x006 c                : 0x0
   +0x008 d                : 0x0
   +0x00c gn               : [6] 0x0
   +0x024 ex               : 0x0 
```

下面的命令显示在地址 0x01002BE0 10 ULONGs 数组：

```dbgcmd
0:000> dt -ca10 ULONG 01002be0 
[0] 0x1001098
[1] 0x1
[2] 0xdead
[3] 0x7d0
[4] 0x1
[5] 0xcd
[6] 0x0
[7] 0x0
[8] 0x0
[9] 0x0 
```

以下命令在不同的地址处继续以前的显示。 请注意"ULONG"不需要重新输入：

```dbgcmd
0:000> dt -ca4 . 01002d00 
Using sym ULONG
[0] 0x12
[1] 0x4ac
[2] 0xbadfeed
[3] 0x2 
```

下面是类型显示的一些示例。 下面的命令的模块中显示所有类型和字符串"MY"开头的全局*thismodule*。 这些带有地址前缀是实际的实例;地址不是类型定义：

```dbgcmd
0:000> dt thismodule!MY* 
010029b8  thismodule!myglobal1
01002990  thismodule!myglobal2
          thismodule!MYCLASS1
          thismodule!MYCLASS2
          thismodule!MYCLASS3
          thismodule!MYTYPE3::u
          thismodule!MYTYPE1
          thismodule!MYTYPE3
          thismodule!MYTYPE3
          thismodule!MYFLAGS 
```

执行类型显示时 **-v**选项可用于显示每个项的大小。 **-S** *大小*选项可用于仅枚举具有特定大小的项。 同样，这些前缀的地址是实际的实例;地址不是类型定义：

```dbgcmd
0:001> dt -s 2 -v thismodule!* 
Enumerating symbols matching thismodule!*, Size = 0x2
Address   Size Symbol
           002 thismodule!wchar_t
           002 thismodule!WORD
           002 thismodule!USHORT
           002 thismodule!SHORT
           002 thismodule!u_short
           002 thismodule!WCHAR
00427a34   002 thismodule!numberOfShips
00427a32   002 thismodule!numberOfPlanes
00427a30   002 thismodule!totalNumberOfItems 
```

下面是举例 **-b**选项。 展开结构和**OwnerThreads**展开数组结构中的，但**Flink**并**闪烁**未遵循列表的指针：

```dbgcmd
kd> dt nt!_ERESOURCE -b 0x8154f040 
   +0x000 SystemResourcesList :  [ 0x815bb388 - 0x816cd478 ]
      +0x000 Flink            : 0x815bb388
      +0x004 Blink            : 0x816cd478
   +0x008 OwnerTable       : (null)
   +0x00c ActiveCount      : 1
   +0x00e Flag             : 8
   +0x010 SharedWaiters    : (null)
   +0x014 ExclusiveWaiters : (null)
   +0x018 OwnerThreads     :
    [00]
      +0x000 OwnerThread      : 0
      +0x004 OwnerCount       : 0
      +0x004 TableSize        : 0
    [01]
      +0x000 OwnerThread      : 0x8167f563
      +0x004 OwnerCount       : 1
      +0x004 TableSize        : 1
   +0x028 ContentionCount  : 0
   +0x02c NumberOfSharedWaiters : 0
   +0x02e NumberOfExclusiveWaiters : 0
   +0x030 Address          : (null)
   +0x030 CreatorBackTraceIndex : 0
   +0x034 SpinLock         : 0
```

下面是举例**dt**在内核模式下。 以下命令将生成输出结果类似于[ **！ process 0 0**](-process.md):

```dbgcmd
kd> dt nt!_EPROCESS -l ActiveProcessLinks.Flink -y Ima -yoi Uni 814856f0 
## ActiveProcessLinks.Flink at 0x814856f0

UniqueProcessId : 0x00000008
ImageFileName : [16] "System"

## ActiveProcessLinks.Flink at 0x8138a030

UniqueProcessId : 0x00000084
ImageFileName : [16] "smss.exe"

## ActiveProcessLinks.Flink at 0x81372368

UniqueProcessId : 0x000000a0
ImageFileName : [16] "csrss.exe"

## ActiveProcessLinks.Flink at 0x81369930

UniqueProcessId : 0x000000b4
ImageFileName : [16] "winlogon.exe"

.... 
```

如果你想要执行的每个元素的列表的命令，使用[ **！ 列表**](-list.md)扩展。

最后， **dt-h**命令将显示简短帮助文本汇总**dt**语法。

 

 





