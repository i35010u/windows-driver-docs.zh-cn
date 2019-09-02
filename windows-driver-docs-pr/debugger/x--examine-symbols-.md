---
title: x（检查符号）
description: X 命令显示与指定的模式匹配的所有上下文中的符号。
ms.assetid: 8c71c2ca-4a9d-43e4-91b3-f05b5475316d
keywords:
- x (检查符号) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- x (Examine Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 126db6c7b4cfdad17a2c0826302a625f267e3485
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866767"
---
# <a name="x-examine-symbols"></a>x（检查符号）


**X**命令显示与指定的模式匹配的所有上下文中的符号。

```dbgcmd
x [Options] Module!Symbol 
x [Options] *
```

## <a name="span-idddk_cmd_examine_symbols_dbgspanspan-idddk_cmd_examine_symbols_dbgspanparameters"></a><span id="ddk_cmd_examine_symbols_dbg"></span><span id="DDK_CMD_EXAMINE_SYMBOLS_DBG"></span>Parameters


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定符号搜索选项。 您可以使用以下一个或多个选项:

<span id="_0"></span> **/0**  
只显示每个符号的地址。

<span id="_1"></span> **/1**  
只显示每个符号的名称。

<span id="_2"></span> **/2**  
只显示每个符号 (而非数据类型) 的地址和名称。

<span id="_D"></span><span id="_d"></span> **/D**  
使用[调试器标记语言](debugger-markup-language-commands.md)显示输出。

<span id="_t"></span><span id="_T"></span> **/t**  
如果数据类型已知, 则显示每个符号的数据类型。

<span id="_v"></span><span id="_V"></span> **/v**  
显示每个符号的符号类型 (本地、全局、参数、函数或未知)。 此选项还显示每个符号的大小。 函数符号的大小是内存中函数的大小。 其他符号的大小是该符号表示的数据类型的大小。 大小始终以字节为单位进行度量并以十六进制格式显示。

<span id="_s_Size"></span><span id="_s_size"></span><span id="_S_SIZE"></span> **/s** *大小*  
仅显示大小 (以字节为单位) 等于*大小*值的符号。 函数符号的*大小*是内存中函数的大小。 其他符号的*大小*是该符号表示的数据类型的大小。 始终显示大小无法确定的符号。 *大小*必须为非零整数。

<span id="_q"></span><span id="_Q"></span> **/q**  
显示带引号格式的符号名称。

<span id="_p"></span><span id="_P"></span> **/p**  
当调试器显示函数名称及其参数时, 省略左括号前的空格。 如果要将函数名称和自变量从**x**显示复制到其他位置, 这种类型的显示可以简化。

<span id="_f"></span><span id="_F"></span> **/f**  
显示函数的数据大小。

<span id="_d"></span><span id="_D"></span> **/d**  
显示数据的数据大小。

<span id="_a"></span><span id="_A"></span> **/a**  
按地址对显示按升序排序。

<span id="_A"></span><span id="_a"></span> **/A**  
按地址降序排序。

<span id="_n"></span><span id="_N"></span> **/n**  
按名称对显示顺序进行升序排序。

<span id="_N"></span><span id="_n"></span> **/N**  
按名称对显示顺序按降序排序。

<span id="_z"></span><span id="_Z"></span> **/z**  
按大小以升序对显示进行排序。

<span id="_Z"></span><span id="_z"></span> **/Z**  
按大小降序排序显示。

<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定要搜索的模块。 此模块可以是 .exe、.dll 或 .sys 文件。 *模块*可以包含各种通配符和说明符。 有关语法的详细信息, 请参阅[字符串通配符语法](string-wildcard-syntax.md)。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span>*符号*   
指定符号必须包含的模式。 *符号*可以包含各种通配符和说明符。 有关语法的详细信息, 请参阅[字符串通配符语法](string-wildcard-syntax.md)。

由于此模式与符号匹配, 因此匹配不区分大小写, 单个前导下划线 (\_) 表示任意数量的前导下划线。 您可以在*符号*内添加空格, 以便您可以指定包含空格的符号名称 (如 "operator new" 或 "Template&lt;A, B&gt;") 而不使用通配符。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>交货</p></td>
<td align="left"><p>用户模式, 内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时, 故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

以下命令将查找 MyModule 中包含字符串 "自旋" 的所有符号。

```dbgcmd
0:000> x mymodule!*spin* 
```

以下命令快速查找 MyModule 中的 "DownloadMinor" 和 "DownloadMajor" 符号。

```dbgcmd
0:000> x mymodule!downloadm??or 
```

你还可以使用以下命令显示 MyModule 中的所有符号。

```dbgcmd
0:000> x mymodule!* 
```

上述命令还强制调试器重载 MyModule 中的符号信息。 如果要使用最小显示重载模块中的符号, 请使用以下命令。

```dbgcmd
0:000> x mymodule!*start* 
```

几个符号始终包含字符串 "start"。 因此, 前面的命令将始终显示某些输出, 以验证该命令是否正常工作。 但前面的命令避免了过多的显示长度**x mymodule\*!** 。

显示显示每个符号的起始地址和完整符号名称。 如果符号是函数名称, 则该显示还包含其参数类型的列表。 如果符号是全局变量, 则显示其当前值。

**X**命令有一种特殊情况。 若要显示当前上下文的所有局部变量的地址和名称, 请使用以下命令。

```dbgcmd
0:000> x * 
```

**请注意**   , 在大多数情况下, 除非已加载私有符号, 否则不能访问局部变量。 有关此情况的详细信息, 请[参阅 dbgerr005:需要](dbgerr005--private-symbols-required.md)私有符号。 若要显示局部变量的值, 请使用[**dv (显示局部变量)** ](dv--display-local-variables-.md)命令。

 

下面的示例演示 **/0**、 **/1**和 **/2**选项。

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

如果要使用**x**命令的输出作为[**foreach**](-foreach.md)命令的输入, 则 **/0**、 **/1**和 **/2**选项非常有用。

```dbgcmd
.foreach ( place { x /0 MyApp!*MySym*} ) { .echo ${place}+0x18 }
```

下面的示例演示用于在模块 notepad.exe 上筛选函数的开关 **/f** 。

```dbgcmd
0:000> x /f /v notepad!*main*
prv func   00000001`00003340  249 notepad!WinMain (struct HINSTANCE__ *, struct HINSTANCE__ *, char *, int)
prv func   00000001`0000a7b0   1c notepad!WinMainCRTStartup$filt$0 (void)
prv func   00000001`0000a540  268 notepad!WinMainCRTStartup (void)
```

使用 **/v**选项时, 显示的第一列显示符号类型 (local、global、parameter、function 或 unknown)。 第二列是符号的地址。 第三列是符号的大小 (以字节为单位)。 第四列显示模块名称和符号名称。 在某些情况下, 此显示后跟一个等号 (=), 然后是符号的数据类型。 还显示符号的源 (公共或完整符号信息)。

```dbgcmd
kd> x /v nt!CmType*
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 806c9e68  150 nt!CmTypeName = struct _UNICODE_STRING [42]
global 806c9e68    0 nt!CmTypeName = struct _UNICODE_STRING []
global 805bd7b0    0 nt!CmTypeString = unsigned short *[]
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

在前面的示例中, 大小以十六进制格式提供, 而数据类型以十进制格式提供。 因此, 在前面的示例的最后一行中, 数据类型是指向无符号短整数的42指针的数组。 此数组的大小为 42\*4 = 168, 168 以十六进制格式显示为0xA8。

您可以使用 * */s** *size* 选项来仅显示大小 (以字节为单位) 为特定值的符号。 例如, 可以将前面的示例中的命令限制为表示大小为0xA8 的对象的符号。

```dbgcmd
kd> x /v /s a8 nt!CmType*
global 805bd7b0   a8 nt!CmTypeString = unsigned short *[42]
```

**使用数据类型**

**/T**选项使调试器显示有关每个符号的数据类型的信息。 请注意, 对于许多符号, 即使没有 **/t**选项, 也会显示此信息。 使用 **/t**时, 此类符号的数据类型信息显示两次。

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

X 命令将显示某个类型的实例。

```dbgcmd
0:001> x foo!MyClassInstance
00f4f354          foo!MyClassInstance = 0x00f78768
```

X 命令不显示任何内容, 只基于类型的名称。

```dbgcmd
0:001> x foo!MyClass
0:001>
```

若要使用类型的名称显示类型信息, 请考虑使用[**dt (显示类型)** ](dt--display-type-.md), 它提供类型和类型实例的信息:

```dbgcmd
0:001> dt foo!MyClass
   +0x000 IntMemberVariable : Int4B
   +0x004 FloatMemberVariable : Float
   +0x008 BoolMemberVariable : Bool
   +0x00c PtrMemberVariable : Ptr32 MyClass
```

**使用模板**

您可以使用包含 x 命令的通配符来显示模板类, 如本示例中所示。

```dbgcmd
0:001>  x Fabric!Common::ConfigEntry*TimeSpan?
000007f6`466a2f9c Fabric!Common::ConfigEntry<Common::TimeSpan>::ConfigEntry<Common::TimeSpan> (void)
000007f6`466a3020 Fabric!Common::ConfigEntry<Common::TimeSpan>::~ConfigEntry<Common::TimeSpan> (void)
```

使用模板时, 请考虑使用[**dt (显示类型)** ](dt--display-type-.md)命令, 因为 x 命令不显示单个模板类项。

```dbgcmd
0:001> dt foo!Common::ConfigEntry<Common::TimeSpan>
   +0x000 __VFN_table : Ptr64 
   +0x008 componentConfig_ : Ptr64 Common::ComponentConfig
   +0x010 section_         : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
   +0x038 key_             : std::basic_string<wchar_t,std::char_traits<wchar_t>,std::allocator<wchar_t> >
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[验证符号](verifying-symbols.md)

[**dv (显示局部变量)** ](dv--display-local-variables-.md)

 

 






