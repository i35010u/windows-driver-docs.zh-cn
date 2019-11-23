---
title: dt（显示类型）
description: Dt 命令显示有关局部变量、全局变量或数据类型的信息。 这会显示有关简单数据类型以及结构和联合的信息。
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
ms.openlocfilehash: fa4ac5a62cd92c108b1c33725dbdc35b0c883f75
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284969"
---
# <a name="dt-display-type"></a>dt（显示类型）


**Dt**命令显示有关局部变量、全局变量或数据类型的信息。 这会显示有关简单数据类型以及结构和联合的信息。

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

## <a name="span-idddk_cmd_display_type_dbgspanspan-idddk_cmd_display_type_dbgspanparameters"></a><span id="ddk_cmd_display_type_dbg"></span><span id="DDK_CMD_DISPLAY_TYPE_DBG"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定运行包含所需信息的进程的处理器。 有关详细信息，请参阅[多处理器语法](multiprocessor-syntax.md)。 只能在内核模式下指定处理器。

<span id="_______DisplayOpts______"></span><span id="_______displayopts______"></span><span id="_______DISPLAYOPTS______"></span>*DisplayOpts*   
指定下表中提供的一个或多个选项。 这些选项前面带有连字符。

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
<td align="left"><p><strong>-a</strong>[<em>数量</em>]</p></td>
<td align="left"><p>在新行上显示每个数组元素及其索引。 将显示 "<em>数量</em>" 元素总数。 介于和<em>数量</em>之间不得有空格 。 如果<strong>-a</strong>后面不是一个数字，则显示数组中的所有项。 <strong>-A</strong>[<em>数量</em>] 开关应紧靠要以这种方式显示的每个类型名称或字段名称之前。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong></p></td>
<td align="left"><p>以递归方式显示块。 如果显示的结构包含子结构，则它将以递归方式展开为任意深度，并显示为完整。 仅当指针在原始结构中而不是在子结构中时才会展开。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>精简输出。 所有字段在一行上显示（如果可能）。 （与<strong>-a</strong>开关一起使用时，每个数组元素都采用一个行，而不是格式化为多行块。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>当与以星号结尾的<em>名称</em>一起使用时，将显示以<em>name</em>开头的所有类型的详细输出。 如果<em>名称</em>不以星号结尾，则显示详细输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>强制执行<strong>dt</strong>来枚举类型。 仅当<strong>dt</strong>错误地将<em>Name</em>值解释为实例而不是类型时，才需要此选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-i</strong></p></td>
<td align="left"><p>不要缩进子类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-o</strong></p></td>
<td align="left"><p>省略结构字段的偏移量值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-p</strong></p></td>
<td align="left"><p><em>Address</em>是物理地址，而不是虚拟地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-r</strong>[<em>深度</em>]</p></td>
<td align="left"><p>以递归方式转储子类型字段。 如果给出了<em>深度</em>，此递归将停止<em>深度</em>级别。 <em>深度</em>必须为1到9之间的数字，并且在<strong>r</strong>和<em>深度</em>之间一定不能有空格。 <strong>-R</strong>[<em>depth</em>] 开关应紧靠在地址之前。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong> <em>大小</em></p></td>
<td align="left"><p>仅枚举大小以字节为单位的类型等于<em>大小</em>的值。 <strong>-S</strong>选项仅在枚举类型时才有用。 如果指定<strong>-s</strong> ，则也始终隐含<strong>-e</strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>仅枚举类型。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>详细输出。 这会提供其他信息，例如结构的总大小及其元素的数目。 当与<strong>-y</strong>搜索选项一起使用时，将显示所有符号，甚至包括没有关联类型信息的符号。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______SearchOpts______"></span><span id="_______searchopts______"></span><span id="_______SEARCHOPTS______"></span>*SearchOpts*   
指定下表中提供的一个或多个选项。 这些选项前面带有连字符。

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
<td align="left"><p>这表明下一个参数是一个名称。 如果下一项完全包含十六进制字符，则应使用此方法，因为它将被视为地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-y</strong></p></td>
<td align="left"><p>这指示下一个参数是名称的开头，而不是整个名称。 包括<strong>-y</strong>时，将列出所有匹配项，后跟列表中第一个匹配项的详细信息。 如果不包含<strong>-y</strong> ，则只显示完全匹配项。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定定义此结构的模块的可选参数。 如果存在与全局变量或类型同名的局部变量或类型，则应包含*module*来指定全局变量。 否则， **dt**命令将显示局部变量，即使本地变量是不区分大小写的匹配并且全局变量是区分大小写的匹配项。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
指定类型或全局变量的名称。 如果*名称*以星号（\*）结尾，则显示所有匹配项的列表。 因此， **Dt A\\** * 将列出所有数据类型、globals 和静态值以 "A" 开头，但不会显示这些类型的实际实例。 （如果同时使用了 **-v**显示选项，则将显示所有符号，而不仅仅是具有关联类型信息的符号。）你还可以使用句点（ **.** ）替换*name* ，以表示你要重复最近使用的*name*值。

如果*名称*包含空格，则应将其括在括号中。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span>*字段*   
指定要显示的字段。 如果省略*字段*，将显示所有字段。 如果*字段*后跟一个句点（ **.** ），则此字段的第一级子字段也将显示。 如果*字段*后跟一系列期间，子字段将显示为与周期数相等的深度。 如果使用了 **-y**搜索选项，则后面跟一个句点的任何字段名称将被视为前缀匹配。 如果*字段*后跟星号（\*），则将其视为只是字段的开头，而不一定是整个字段，并显示所有匹配字段。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*Address*   
指定要显示的结构的地址。 如果省略*Name* ，则必须包含*address*并且必须指定全局变量的地址。 除非另行指定，否则*地址*被视为虚拟地址。 使用 **-p**选项来指定物理地址。 使用 "at" 符号（ **@** ）来指定寄存器（例如， <strong>@eax</strong>）。

<span id="_______List______"></span><span id="_______list______"></span><span id="_______LIST______"></span>*列出*   
指定链接列表链接的字段名称。 *Address*参数必须包括在内。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

**Dt**命令输出将始终以10为基数显示有符号数字，并以十六进制形式表示无符号数字。

允许符号值的**dt**的所有参数也允许字符串通配符。 有关详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

**-Y**和 **-n**选项可以位于任何*名称*或*字段*之前。 **-Y**选项允许指定类型或结构名称的开头。 例如， **dt-y ALLEN**将显示有关**ALLENTOWN**类型的数据。 但是，不能使用**dt-y**显示类型**ALLENTOWN** 。相反，您必须使用**dt-Ny a** **，因为是有效的十六进制**值，并且将被解释为不带 **-n**选项的地址。

如果*Name*表示结构，则将显示所有字段（例如， **dt mystruct>)** ）。 如果只需要一个特定字段，可以执行**Dt Mystruct>) myField**。 这将显示 C 调用**myField**的成员。 但请注意，命令**Dt Mystruct>) MyField1 myField2**显示**mystruct>). myField1**和**mystruct>)** 。 它不显示**mystruct>). myField1. myField2**。

如果结构名称或字段后跟下标，则它指定数组的单个实例。 例如， **Dt Mystruct>) myFieldArray\[3\]** 将显示相关数组的第四个元素。 但如果类型名称后跟下标，则会指定整个数组。 例如， **DT CHAR\[8\] myPtr**将显示八个字符的字符串。 无论当前基数如何，下标始终采用 decimal 形式;**0x**前缀将导致错误。

由于该命令使用中的类型信息。*pdb*文件，可以自由地用于调试任何 CPU 平台。

**Dt**使用的类型信息包括使用**typedef**创建的所有类型名称，包括所有 Windows 定义的类型。 例如，**无符号长**字符**和字符**不是有效的类型名称，但**ULONG**和**char**是。 有关所有 Windows 类型名称的完整列表，请参阅 Microsoft Windows SDK。

只要你的程序中实际使用了这些类型，则你自己的代码中的**typedef**所创建的所有类型都将存在。 但是，在标头中定义但从不实际使用的类型不会存储在 .pdb 符号文件中，并且调试器将无法访问这些类型。 若要使此类类型可用于调试器，请将其用作**typedef**语句的*输入*。 例如，如果你的代码中显示以下内容，则结构\_的数据将存储在 .pdb 符号文件中，并且可以通过**dt**命令显示：

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA;
typedef  MY_DATA *PMY_DATA; 
```

另一方面，以下代码无法满足这一要求，因为我\_的数据和 PMY\_数据都是由初始**typedef**定义的，因此，我的\_数据本身并未用作任何**typedef**语句的输入：

```dbgcmd
typedef struct _MY_DATA {
    . . .
    } MY_DATA, *PMY_DATA; 
```

在任何情况下，类型信息仅包含在完整的符号文件中，而不是已去除所有私有符号信息的符号文件中。 有关详细信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

如果要显示 unicode 字符串，则需先使用[ **。 enable\_unicode （启用 Unicode 显示）** ](-enable-unicode--enable-unicode-display-.md)命令。 您可以使用来控制长整数的显示[ **。 "启用\_long\_status （启用长整数显示）** ](-enable-long-status--enable-long-integer-display-.md)命令。

在下面的示例中， **dt**显示了一个全局变量：

```dbgcmd
0:000> dt mt1 
   +0x000 a                : 10
   +0x004 b                : 98 'b'
   +0x006 c                : 0xdd
   +0x008 d                : 0xabcd
   +0x00c gn               : [6] 0x1
   +0x024 ex               : 0x0 
```

在下面的示例中， **dt**显示数组字段**gn**：

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

以下命令显示变量的一些子字段：

```dbgcmd
0:000> dt mcl1 m_t1 dpo 
   +0x010 dpo  : DEEP_ONE
   +0x070 m_t1 : MYTYPE1 
```

以下命令显示字段**m\_t1**的子字段。 因为句点会自动导致前缀匹配，所以这还会显示以 "m\_t1" 开头的任何字段的子字段：

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

您可以对任何深度重复此操作。 例如，命令**dt mcl1c.** 将显示深度为四的所有字段，以便第一个字段名称以开头 **，第**三个字段名称以**c**开头。

下面是有关如何显示子字段的更详细示例。 首先，显示 " **Ldr** " 字段：

```dbgcmd
0:000> dt nt!_PEB Ldr 7ffdf000 
   +0x00c Ldr : 0x00191ea0 
```

现在，展开 "指针类型" 字段：

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

现在显示 " **CriticalSectionTimeout** " 字段：

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout 7ffdf000 
   +0x070 CriticalSectionTimeout : _LARGE_INTEGER 0xffffe86d`079b8000 
```

现在，展开深度为一级的**CriticalSectionTimeout**结构子字段：

```dbgcmd
0:000> dt nt!_PEB CriticalSectionTimeout. 7ffdf000 
   +0x070 CriticalSectionTimeout  :  0xffffe86d`079b8000
      +0x000 LowPart                 : 0x79b8000
      +0x004 HighPart                : -6035
      +0x000 u                       : __unnamed
      +0x000 QuadPart                : -25920000000000 
```

现在，展开 " **CriticalSectionTimeout**结构" 子字段 "深度" 级别：

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

以下命令显示位于地址0x0100297C 的数据类型 MYTYPE1 的实例：

```dbgcmd
0:000> dt 0x0100297c MYTYPE1 
   +0x000 a                : 22
   +0x004 b                : 43 '+'
   +0x006 c                : 0x0
   +0x008 d                : 0x0
   +0x00c gn               : [6] 0x0
   +0x024 ex               : 0x0 
```

以下命令在地址0x01002BE0 显示 10 ULONGs 的数组：

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

以下命令将继续在不同的地址上显示。 请注意，不需要重新输入 "ULONG"：

```dbgcmd
0:000> dt -ca4 . 01002d00 
Using sym ULONG
[0] 0x12
[1] 0x4ac
[2] 0xbadfeed
[3] 0x2 
```

下面是类型显示的一些示例。 以下命令将显示模块*thismodule*中以字符串 "MY" 开头的所有类型和全局。 带有地址的前缀是实际实例;没有地址的那些类型为类型定义：

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

执行类型显示时，可以使用 **-v**选项来显示每个项目的大小。 **-S** *size*选项仅可用于枚举特定大小的项目。 同样，带有地址的前缀是实际实例;没有地址的那些类型为类型定义：

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

下面是 **-b**选项的示例。 该结构已展开，并扩展了结构中的**OwnerThreads**数组，但未遵循**Flink**和**闪烁**列表指针：

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

下面是内核模式下的**dt**的示例。 以下命令生成类似于[ **！ process 0 0**](-process.md)的结果：

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

如果要对列表中的每个元素执行命令，请使用[ **！ list**](-list.md)扩展。

最后， **dt-h**命令将显示简短的帮助文本，以概述**dt**语法。

 

 





