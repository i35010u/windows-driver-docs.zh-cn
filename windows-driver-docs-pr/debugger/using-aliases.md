---
title: 使用别名
description: 使用别名
ms.assetid: ee0540d0-5bfd-47ef-92b1-ec1d6954aec7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ccd9591a1dae66008545a28b85ea37407440f6a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349766"
---
# <a name="using-aliases"></a>使用别名


## <span id="ddk_using_aliases_dbg"></span><span id="DDK_USING_ALIASES_DBG"></span>


*别名*都是自动替换为其他字符字符串的字符字符串。 在调试器命令，以避免重新键入某些常见的短语，可以使用它们。

别名组成*别名*和一个*别名等效*。 当调试器命令的一部分使用的别名名称时，名称将自动替换为别名等效项。 这种替换会立即发生之前分析或执行该命令。

调试器支持三种类型的别名：

-   设置并将其命名*名用户为别名*。

-   可以设置*修复名称的别名*，但它们被命名为**美元 u0**，**美元 u1**，...，**美元 u9**。

-   调试器设置和名称*自动别名*。

### <a name="span-iddefiningausernamedaliasspanspan-iddefiningausernamedaliasspandefining-a-user-named-alias"></a><span id="defining_a_user_named_alias"></span><span id="DEFINING_A_USER_NAMED_ALIAS"></span>定义名为用户的别名

在定义名为用户的别名时，可以选择别名名称和别名等效项：

-   别名名称可以是任何不包含空格的字符串。

-   等效的别名可以是任何字符串。 如果在键盘输入它，等效的别名不能包含前导空格或回车。 或者，您可以将它设置为一个字符串，在内存中，数值表达式的值的环境变量或一个或多个调试器命令的输出的文件的内容的值。

区分大小写的别名名称和别名等效项。

若要定义或重新定义名为用户的别名，请使用[ **（设置别名） 作为**](as--as--set-alias-.md)或 **（设置别名） 作为**命令。

若要删除别名，请使用[ **ad （删除别名）** ](ad--delete-alias-.md)命令。

若要列出所有当前用户命名别名，请使用[ **al （列表别名）** ](al--list-aliases-.md)命令。

### <a name="span-iddefiningafixednamealiasspanspan-iddefiningafixednamealiasspandefining-a-fixed-name-alias"></a><span id="defining_a_fixed_name_alias"></span><span id="DEFINING_A_FIXED_NAME_ALIAS"></span>定义的固定名称别名

有 10 个固定名称的别名。 是其别名**美元 u0**，**美元 u1**，...，**美元 u9**。 对应的别名可以是任何字符串不包含 ENTER 键击。

使用[ **r （寄存器）** ](r--registers-.md)命令，以便定义固定名称的别名为等效的别名。 在定义的固定名称别名时，必须插入句点 (**。**) 的字母"u"前。 别名等号 （=） 后的文本等效。 等效的别名可以包含空格或分号，但会忽略前导空格和尾随空格。 不应将别名等效括在引号 （除非您想在结果中的引号）。

**请注意**  不要执行使用相混淆**r （寄存器）** 命令的固定名称的别名。 这些别名不是寄存器或伪寄存器中，即使你使用**r**命令以设置其别名等效项。 无需添加在 (**@**) 登录之前这些别名，并且您不能使用**r**命令*显示*这些别名之一的值。

 

默认情况下，如果未定义的固定名称别名，它将为空字符串。

### <a name="span-idautomaticaliasesspanspan-idautomaticaliasesspanautomatic-aliases"></a><span id="automatic_aliases"></span><span id="AUTOMATIC_ALIASES"></span>自动别名

调试器设置以下自动别名。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">别名名称</th>
<th align="left">别名等效项</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$ntnsym</strong></p></td>
<td align="left"><p>用于在计算机的本机体系结构上的 NT 符号的最合适模块。 此别名可以等于任一<strong>ntdll</strong>或<strong>nt</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ntwsym</strong></p></td>
<td align="left"><p>用于在 32 位调试期间的 NT 符号的最合适模块，使用 WOW64。 此别名可能<strong>ntdll32</strong>或某些其他 32 位版本的 Ntdll.dll。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ntsym</strong></p></td>
<td align="left"><p>用于匹配当前计算机模式下的 NT 符号的最合适的模块。 在纯模式下调试时，此别名是与相同<strong>$ntnsym</strong>。 在非本机模式下调试时，调试器会尝试查找与此模式匹配的模块。 (例如，32 位在调试期间使用 WOW64，此别名等同于<strong>$ntwsym</strong>。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$CurrentDumpFile</strong></p></td>
<td align="left"><p>调试程序加载的最后一个转储文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$CurrentDumpPath</strong></p></td>
<td align="left"><p>上次加载的转储文件的目录路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$CurrentDumpArchiveFile</strong></p></td>
<td align="left"><p>最后一个转储存档文件 （CAB 文件） 加载的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$CurrentDumpArchivePath</strong></p></td>
<td align="left"><p>最后一个转储存档文件 （CAB 文件） 加载目录路径。</p></td>
</tr>
</tbody>
</table>

 

自动的别名为类似于[自动伪寄存器](pseudo-register-syntax.md)，但也可以使用与别名相关令牌使用自动别名 (如 **$ {}**)，而这些都不能使用伪寄存器令牌。

### <a name="span-idusinganaliasinthedebuggercommandwindowspanspan-idusinganaliasinthedebuggercommandwindowspanusing-an-alias-in-the-debugger-command-window"></a><span id="using_an_alias_in_the_debugger_command_window"></span><span id="USING_AN_ALIAS_IN_THE_DEBUGGER_COMMAND_WINDOW"></span>在调试器命令窗口中使用别名

定义别名后，可以使用它在任何命令项中。 别名名称会自动替换与别名对应。 因此，您可以使用别名作为表达式或宏。

别名扩展正确，即使它用引号引起来。 由于别名等效项可以包含任意数量的引号或分号，别名等效项可以表示多个命令。

仅当其名称由空格分隔从其他字符被识别用户命名的别名。 其别名名称的第一个字符必须开始的行，或者按照空格、 分号或一个引号。 其别名名称的最后一个字符必须结束行或后跟一个空格、 分号或一个引号。

**请注意**  输入到任何文本[调试器命令窗口](debugger-command-window.md)开头"as"，"为"，"ad"或"al"不会接收别名替换。 此限制可以防止呈现不可操作的别名命令。 此限制，但是也意味着命令后面**ad**或**al**行上没有替换为各自的别名。 如果你想要替换这些字符串之一开头的行中的别名，添加该别名前的一个分号。

 

但是，可以使用 **$ {}** 令牌以展开用户命名的别名，即使它是其他文本旁边。 此外可以使用某些开关以及此令牌，以免别名扩展或显示某些与别名相关的值。 有关这些情况的详细信息，请参阅[ **$ {} （别名解释器）**](-------alias-interpreter-.md)。

固定名称别名扩展正确从行中，而不考虑如何嵌入在行的文本中的任意位置。

不能使用仅在 WinDbg 中可用的命令 ([**打开**](-open--open-source-file-.md)， [ **.write\_cmd\_hist （编写命令历史记录）** ](-write-cmd-hist--write-command-history-.md)， [ **.lsrcpath**](-srcpath---lsrcpath--set-source-path-.md)，和[ **.lsrcfix**](-srcfix---lsrcfix--use-source-server-.md)) 和几个其他命令 ([**.hh ***](-hh--open-html-help-file-.md)， [ **.cls**](-cls--clear-screen-.md)， [ **.wtitle**](-wtitle--set-window-title-.md)， [**.remote**](-remote--create-remote-exe-server-.md)，内核模式[ **.restart**](-restart--restart-kernel-connection-.md)，和用户模式[ **.restart** ](-restart--restart-target-application-.md))使用别名。

### <a name="span-idusinganaliasinascriptfilespanspan-idusinganaliasinascriptfilespanusing-an-alias-in-a-script-file"></a><span id="using_an_alias_in_a_script_file"></span><span id="USING_AN_ALIAS_IN_A_SCRIPT_FILE"></span>在脚本文件中使用别名

在脚本文件中使用别名时，您必须特别留意以确保在正确的时间已展开别名。 请看以下脚本：

```text
.foreach (value {dd 610000 L4})
{
   as /x ${/v:myAlias} value + 1
   .echo value myAlias
}

ad myAlias
```

第一次循环时， [**一样，（设置别名） 作为**](as--as--set-alias-.md)命令将值分配给 myAlias。 分配给 myAlias 的值是 1 加 610000 （dd 命令的第一个输出）。 但是，当[ **.echo （Echo 注释）** ](-echo--echo-comment-.md)执行命令、 myAlias 未尚未展开，因此我们看到文本"myAlias"而不是 610001。

```dbgcmd
0:001> $$>< c:\Script02.txt
00610000 myAlias
00905a4d 0x610001
00000003 0x905a4e
00000004 0x4
0000ffff 0x5
```

问题在于该 myAlias 不展开直到输入一个新的代码块。 向循环的下一个条目是新的块，因此 myAlias 获取扩展到 610001。 那就太晚，但是： 我们已经看到 610001 第一次循环时，不是第二个时间。我们可以解决此问题，通过封闭[ **.echo （Echo 注释）** ](-echo--echo-comment-.md)命令在新的块中，以下脚本中所示。

```text
.foreach (value {dd 610000 L4}) 
{
   as /x ${/v:myAlias} value + 1
   .block{.echo value myAlias}
}

ad myAlias
```

与更改的脚本，我们将获得以下正确输出值。

```dbgcmd
0:001> $$>< c:\Script01.txt
00610000 0x610001
00905a4d 0x905a4e
00000003 0x4
00000004 0x5
0000ffff 0x10000
```

有关详细信息，请参阅[ **.block** ](-block.md)并[ **$ {} （别名解释器）**](-------alias-interpreter-.md)。

### <a name="span-idusingaforeachtokeninanaliasspanspan-idusingaforeachtokeninanaliasspanspan-idusingaforeachtokeninanaliasspanusing-a-foreach-token-in-an-alias"></a><span id="Using_a_.foreach_Token_in_an_Alias"></span><span id="using_a_.foreach_token_in_an_alias"></span><span id="USING_A_.FOREACH_TOKEN_IN_AN_ALIAS"></span>在别名中使用.foreach 令牌

当你使用[ **.foreach** ](-foreach.md)别名的定义中的令牌，则必须特别留意以确保令牌已展开。 请考虑下面的命令序列。

```dbgcmd
r $t0 = 5
ad myAlias
.foreach /pS 2 /ps 2 (Token {?@$t0}) {as myAlias Token}
al
```

第一个命令设置的值**美元 t0**伪寄存器为 5。 第二个命令将删除可能已以前分配给 myAlias 任何值。 第三个命令将第三个标记的 **？ @$ t0**命令，并尝试将该令牌的值分配给 myAlias。 第四个命令将列出所有别名及其值。 我们期望的值 myAlias 为 5，而值是"令牌"一词。

```dbgcmd
   Alias            Value  
 -------          ------- 
 myAlias          Token 
```

问题在于[**作为**](as--as--set-alias-.md)命令的正文中的行的开头是[ **.foreach** ](-foreach.md)循环。 在行开头**作为**命令时，别名和令牌，不展开行。 如果我们将以分号或之前的空格**作为**命令，然后展开任何别名或已经具有值的令牌。 在此示例中，因为已具有一个值，才会展开 myAlias。 令牌会展开，因为它具有的值为 5。 下面是通过前一个分号添加相同的命令序列**作为**命令。

```dbgcmd
r $t0 = 5
ad myAlias
.foreach /pS 2 /ps 2 (Token {?@$t0}) {;as myAlias Token}
al
```

现在，我们得到了预期的输出。

```dbgcmd
  Alias            Value  
 -------          ------- 
 myAlias          5 
```

### <a name="span-idrecursivealiasesspanspan-idrecursivealiasesspanrecursive-aliases"></a><span id="recursive_aliases"></span><span id="RECURSIVE_ALIASES"></span>递归的别名

可以定义任何别名中使用的固定名称别名。 此外可以修复名称别名的定义中使用用户命名的别名。 但是，若要在另一名用户为别名的定义中使用用户命名的别名，您需要添加分号前的**作为**或**作为**命令，否则别名替换不会出现在该行上。

当使用此类型的递归定义时，每个别名会转换就立即使用它。 例如，下面的示例显示**3**，而非**7**。

```dbgcmd
0:000> r $.u2=2 
0:000> r $.u1=1+$u2 
0:000> r $.u2=6 
0:000> ? $u1 
Evaluate expression: 3 = 00000003
```

同样，下面的示例显示**3**，而非**7**。

```dbgcmd
0:000> as fred 2 
0:000> r $.u1= 1 + fred 
0:000> as fred 6 
0:000> ? $u1 
Evaluate expression: 3 = 00000003
```

以下示例还允许使用并显示**9**。

```dbgcmd
0:000> r $.u0=2 
0:000> r $.u0=7+$u0 
0:000> ? $u0
Evaluate expression: 9 = 00000009
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

因此，不需要键入长或者过于复杂的符号名称，如以下示例所示，可以使用别名。

```dbgcmd
0:000> as Short usersrv!NameTooLongToWantToType
0:000> dw Short +8
```

下面的示例类似于前面的示例中，但它使用固定名称别名。

```dbgcmd
0:000> r $.u0=usersrv!NameTooLongToWantToType
0:000> dw $u0+8
```

经常使用的命令，可作为宏使用别名。 下面的示例递增**eax**并**ebx**注册两次。

```dbgcmd
0:000> as GoUp r eax=eax+1; r ebx=ebx+1
0:000> GoUp
0:000> GoUp
```

下面的示例使用别名来简化键入的命令。

```dbgcmd
0:000> as Cmd "dd esp 14; g"
0:000> bp MyApi Cmd 
```

下面的示例类似于前面的示例中，但它使用固定名称别名。

```dbgcmd
0:000> r $.u5="dd esp 14; g"
0:000> bp MyApi $u5 
```

前面的示例都等效于以下命令。

```dbgcmd
0:000> bp MyApi "dd esp 14; g"
```

### <a name="span-idtoolsinifilespanspan-idtoolsinifilespan-toolsini-file"></a><span id="tools_ini_file"></span><span id="TOOLS_INI_FILE"></span> Tools.ini 文件

在 CDB （和 NTSD） 中，您可以预定义中的固定名称别名[tools.ini](configuring-tools-ini.md)文件。 若要预定义的固定名称别名，将添加 **$u**到所需的字段你\[NTSD\]条目，如以下示例所示。

```ini
[NTSD]
$u1:_ntdll!_RtlRaiseException
$u2:"dd esp 14;g"
$u9:$u1 + 42
```

Tools.ini 文件中，无法设置用户命名别名。

### <a name="span-idfixednamealiasesvsusernamedaliasesspanspan-idfixednamealiasesvsusernamedaliasesspanfixed-name-aliases-vs-user-named-aliases"></a><span id="fixed_name_aliases_vs__user_named_aliases"></span><span id="FIXED_NAME_ALIASES_VS__USER_NAMED_ALIASES"></span>固定名称的别名 vs。用户命名别名

用户名称的别名为固定的名为别名比易于使用。 其定义语法更简单，且可以使用列出它们[ **al （列表别名）** ](al--list-aliases-.md)命令。

如果使用其他文本旁边，替换固定命名别名。 若要使其他文本旁边时被替换的用户命名别名，请将其括在[ **$ {} （别名解释器）** ](-------alias-interpreter-.md)令牌。

在用户命名别名替换之前执行了固定名称别名替换。

 

 





