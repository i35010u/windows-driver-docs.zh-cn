---
title: x （检查符号）
description: X 命令显示所有与指定的模式匹配的上下文中的符号。
ms.assetid: 8c71c2ca-4a9d-43e4-91b3-f05b5475316d
keywords:
- x （检查符号） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- x (Examine Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14cf8fe0e8af0ae4eefd8de0b99998e00c7d6284
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540492"
---
# <a name="x-examine-symbols"></a>x （检查符号）


**X**命令显示所有与指定的模式匹配的上下文中的符号。

```dbgcmd
x [Options] Module!Symbol 
x [Options] *
```

## <a name="span-idddkcmdexaminesymbolsdbgspanspan-idddkcmdexaminesymbolsdbgspanparameters"></a><span id="ddk_cmd_examine_symbols_dbg"></span><span id="DDK_CMD_EXAMINE_SYMBOLS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定符号搜索选项。 可以使用一个或多个以下选项：

<span id="_0"></span>**/0**  
显示仅每个符号的地址。

<span id="_1"></span>**/1**  
显示仅每个符号的名称。

<span id="_2"></span>**/2**  
显示的地址和每个符号 （而不是数据类型） 的名称。

<span id="_D"></span><span id="_d"></span>**/D**  
显示输出使用[调试器标记语言](debugger-markup-language-commands.md)。

<span id="_t"></span><span id="_T"></span>**/t**  
如果数据类型已知时，显示的数据类型的每个符号。

<span id="_v"></span><span id="_V"></span>**/v**  
显示每个符号的符号类型 （本地、 全局、 参数、 函数或未知）。 此选项还显示每个符号的大小。 是函数符号的大小是在内存中函数的大小。 其他符号的大小是符号表示的数据类型的大小。 大小始终以字节为单位，并以十六进制格式显示。

<span id="_s_Size"></span><span id="_s_size"></span><span id="_S_SIZE"></span>**/s** *大小*  
显示仅这些符号的大小 （字节），等于的值*大小*。 *大小*函数的符号是在内存中函数的大小。 *大小*的其他符号是符号表示的数据类型的大小。 始终显示的符号不能确定其大小。 *大小*必须为非零的整数。

<span id="_q"></span><span id="_Q"></span>**/q**  
显示符号中带引号的形式的名称。

<span id="_p"></span><span id="_P"></span>**/p**  
当调试器将显示函数名称和其自变量时，请省略左括号前的空间。 显示此类可以更轻松如果函数名称和中的自变量将复制**x**到另一个位置显示。

<span id="_f"></span><span id="_F"></span>**/f**  
显示函数的数据大小。

<span id="_d"></span><span id="_D"></span>**/d**  
显示数据的数据大小。

<span id="_a"></span><span id="_A"></span>**/a**  
对显示的地址，以升序进行排序。

<span id="_A"></span><span id="_a"></span>**/A**  
对显示的地址，以降序进行排序。

<span id="_n"></span><span id="_N"></span>**/n**  
对显示的名称，按升序进行排序。

<span id="_N"></span><span id="_n"></span>**/N**  
对显示的名称，以降序进行排序。

<span id="_z"></span><span id="_Z"></span>**/z**  
对显示的大小，按升序进行排序。

<span id="_Z"></span><span id="_z"></span>**/Z**  
对显示的大小，以降序进行排序。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定要搜索的模块。 此模块可以是.exe、.dll 或.sys 文件。 *模块*可以包含各种通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *符号*   
指定必须包含符号的模式。 *符号*可以包含各种通配符和说明符。 有关语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

与符号匹配此模式，因为匹配时不区分大小写，并在单个前导下划线 (\_) 表示任意数量的前导下划线。 可以添加内的空格*符号*，以便您可以指定包含空格的符号名 (如"operator new"或"模板&lt;A，B&gt;") 而无需使用通配符字符。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

以下命令将查找的所有符号中包含字符串"旋转"MyModule。

```dbgcmd
0:000> x mymodule!*spin* 
```

以下命令快速 MyModule 中查找"DownloadMinor"和"DownloadMajor"符号。

```dbgcmd
0:000> x mymodule!downloadm??or 
```

通过使用以下命令，还可以 MyModule 显示所有符号。

```dbgcmd
0:000> x mymodule!* 
```

前面的命令也迫使调试程序来重新加载 MyModule 中的符号信息。 如果你想要重新加载该模块中带有最少显示的符号，使用以下命令。

```dbgcmd
0:000> x mymodule!*start* 
```

一些符号始终包含字符串"启动"。 因此，前面的命令始终显示一些输出以验证命令正常工作。 但在前面的命令可避免过多的显示长度的 * * x mymodule ！\\***.

屏幕将显示每个符号和完整符号名称的起始地址。 如果符号为函数名称，显示内容还包括其参数类型的列表。 如果符号为全局变量，显示其当前值。

没有其他的一个特例**x**命令。 若要显示的地址和所有本地变量的当前上下文的名称，请使用以下命令。

```dbgcmd
0:000> x * 
```

**请注意**  在大多数情况下，不能访问本地变量，除非已加载私有符号。 有关这种情况的详细信息，请参阅[dbgerr005:需要私有符号](dbgerr005--private-symbols-required.md)。 若要显示的本地变量的值，请使用[ **dv （显示本地变量）** ](dv--display-local-variables-.md)命令。

 

下面的示例阐释 **/0**， **/1**，并 **/2**选项。

```dbgcmd
0:000:x86> x /0 MyApp!Add*
00b51410          
00b513d0 
      
0:000:x86> x /1 MyApp!Add*
MyApp!AddThreeIntegers
MyApp!AddTwoIntegers

0:000:x86> x /2 MyApp!Add*
00b51410          MyApp!AddThreeIntegers
00b513d0          MyApp!AddTwoIntegers
```

**/0**， **/1**，并 **/2**选项，如果你想要使用的输出有用**x**命令作为输入[ **.foreach** ](-foreach.md)命令。

```dbgcmd
.foreach ( place { x /0 MyApp!*MySym*} ) { .echo ${place}+0x18 }
```

下面的示例演示了该交换机 **/f**时用来筛选器模块 notepad.exe 的函数。

```dbgcmd
0:000> x /f /v notepad!*main*
prv func   00000001`00003340  249 notepad!WinMain (struct HINSTANCE__ *, struct HINSTANCE__ *, char *, int)
prv func   00000001`0000a7b0   1c notepad!WinMainCRTStartup$filt$0 (void)
prv func   00000001`0000a540  268 notepad!WinMainCRTStartup (void)
```

当你使用 **/v**选项，显示的第一列显示的符号类型 （本地、 全局、 参数、 函数或未知）。 第二列是符号的地址。 第三列是符号，以字节为单位的大小。 第四列显示模块名称和符号名称。 在某些情况下，此显示后跟一个等号 （=），然后该符号的数据类型。 此外会显示符号 （公共或完整符号信息） 的源。

```dbgcmd
kd> x /v nt!CmType*
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 806c9e68  150 nt!CmTypeName = struct _UNICODE_STRING [42]
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 805bd7b0    0 nt!CmTypeString = unsigned short *[]
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

在前面的示例中，给定大小以十六进制格式，而在十进制格式中指定的数据类型。 因此，在前面中的最后一行中的数据类型是示例的 42 指向无符号短整数的数组。 此数组的大小是 42\*4 = 168 和 168 作为 0xA8 十六进制格式显示。

可以使用 **/s * * * 大小*选项以显示这些符号的大小 （字节），仅为某个特定值。 例如，可以限制在前面的示例符号表示其大小是 0xA8 对象的命令。

```dbgcmd
kd> x /v /s a8 nt!CmType*
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

**使用数据类型**

**/T**选项会导致调试器显示有关每个符号的数据类型的信息。 请注意，许多符号，此信息显示甚至不带 **/t**选项。 当你使用 **/t**，此类的符号拥有两次显示其数据类型信息。

```dbgcmd
0:001> x prymes!__n*
00427d84 myModule!__nullstring = 0x00425de8 "(null)"
0042a3c0 myModule!_nstream = 512
Type information missing error for _nh_malloc
004021c1 myModule!MyStructInstance = struct MyStruct
00427d14 myModule!_NLG_Destination = <no type information>

0:001> x /t prymes!__n*
00427d84 char * myModule!__nullstring = 0x00425de8 "(null)"
0042a3c0 int myModule!_nstream = 512
Type information missing error for _nh_malloc
004021c1 struct MyStruct myModule!MyStructInstance = struct MyStruct
00427d14 <NoType> myModule!_NLG_Destination = <no type information>
```

X 命令将显示一种类型的实例。

```dbgcmd
0:001> x foo!MyClassInstance
00f4f354          foo!MyClassInstance = 0x00f78768
```

X 命令不显示任何内容基于只是一种类型的名称。

```dbgcmd
0:001> x foo!MyClass
0:001>
```

若要显示使用的类型名称的类型信息，请考虑使用[ **dt （显示类型）**](dt--display-type-.md)，它提供的类型和类型的实例信息：

```dbgcmd
0:001> dt foo!MyClass
   +0x000 IntMemberVariable : Int4B
   +0x004 FloatMemberVariable : Float
   +0x008 BoolMemberVariable : Bool
   +0x00c PtrMemberVariable : Ptr32 MyClass
```

**使用模板**

可以使用通配符使用 x 命令，以显示模板类，在此示例中所示。

```dbgcmd
0:001>  x Fabric!Common::ConfigEntry*TimeSpan?
000007f6`466a2f9c Fabric!Common::ConfigEntry<Common::TimeSpan>::ConfigEntry<Common::TimeSpan> (void)
000007f6`466a3020 Fabric!Common::ConfigEntry<Common::TimeSpan>::~ConfigEntry<Common::TimeSpan> (void)
```

请考虑使用[ **dt （显示类型）** ](dt--display-type-.md)命令使用模板时，因为 x 命令不会显示各个模板类项。

```dbgcmd
0:001> dt foo!Common::ConfigEntry<Common::TimeSpan>
   +0x000 __VFN_table : Ptr64 
   +0x008 componentConfig_ : Ptr64 Common::ComponentConfig
   +0x010 section_         : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
   +0x038 key_             : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[验证符号](verifying-symbols.md)

[**dv （显示本地变量）**](dv--display-local-variables-.md)

 

 






