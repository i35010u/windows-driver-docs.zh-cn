---
title: 使用别名
description: 使用别名
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a25bb8ff701f1520e391df527babf47cc39ab27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803191"
---
# <a name="using-aliases"></a>使用别名


## <span id="ddk_using_aliases_dbg"></span><span id="DDK_USING_ALIASES_DBG"></span>


*别名* 是自动替换为其他字符串的字符串。 可以在调试器命令中使用这些方法，避免重新键入某些常用短语。

别名由 *别名* 和 *等效的别名* 组成。 使用别名作为调试器命令的一部分时，会自动将该名称替换为等效的别名。 此替换将在分析或执行命令之前立即发生。

调试器支持以下三种类型的别名：

-   你可以设置和命名 *用户命名的别名*。

-   你可以设置 *固定名称的别名*，但它们被命名为 **$u 0**， **$u 1**，...， **$u 9**。

-   调试器设置并命名 *自动别名*。

### <a name="span-iddefining_a_user_named_aliasspanspan-iddefining_a_user_named_aliasspandefining-a-user-named-alias"></a><span id="defining_a_user_named_alias"></span><span id="DEFINING_A_USER_NAMED_ALIAS"></span>定义 User-Named 别名

定义用户命名别名时，可以选择别名和等效的别名：

-   别名可以是不包含空格的任何字符串。

-   等效的别名可以是任意字符串。 如果你在键盘上输入它，则等效的别名不能包含前导空格或回车符。 另外，还可以将其设置为与内存中的字符串、数值表达式的值、某个环境变量的值，或者一个或多个调试器命令的输出。

别名和等效的别名都区分大小写。

若要定义或重新定义用户命名的别名，请使用 [**as (Set alias)**](as--as--set-alias-.md) 或 **As (set alias)** 命令。

若要删除别名，请使用 [**ad (Delete alias)**](ad--delete-alias-.md) 命令。

若要列出所有当前用户命名的别名，请使用 [**(列出别名)**](al--list-aliases-.md) 命令。

### <a name="span-iddefining_a_fixed_name_aliasspanspan-iddefining_a_fixed_name_aliasspandefining-a-fixed-name-alias"></a><span id="defining_a_fixed_name_alias"></span><span id="DEFINING_A_FIXED_NAME_ALIAS"></span>定义 Fixed-Name 别名

有10个固定名称的别名。 别名的名称为 **$u 0**， **$u 1**，...， **$u 9**。 它们的别名等效项可以是不包含 ENTER 键的任何字符串。

使用 [**r (寄存器)**](r--registers-.md) 命令为固定名称别名定义等效的别名。 定义固定名称别名时，必须在字母 "u"**之前 () 插入句点。** 等号后的文本 (=) 是等效的别名。 等效的别名可以包含空格或分号，但会忽略前导空格和尾随空格。 不应将别名中的等效项括在引号 (中，除非在结果) 中需要用引号引起来。

**注意**   不要使用 r (为固定名称别名 **注册)** 命令。 这些别名不是寄存器或伪寄存器，即使使用 **r** 命令设置其别名等效项也是如此。 不需要在这些别名前面添加 at (**@**) 符号，也不能使用 **r** 命令 *显示* 其中一个别名的值。

 

默认情况下，如果未定义固定名称别名，则该别名为空字符串。

### <a name="span-idautomatic_aliasesspanspan-idautomatic_aliasesspanautomatic-aliases"></a><span id="automatic_aliases"></span><span id="AUTOMATIC_ALIASES"></span>自动别名

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
<td align="left"><p>计算机的本机体系结构上最适合用于 NT 符号的模块。 此别名可以等于 <strong>ntdll.dll</strong> 或 <strong>nt</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ntwsym</strong></p></td>
<td align="left"><p>使用 WOW64 的32位调试期间最适合 NT 符号的模块。 此别名可以是 <strong>ntdll32</strong> 或 Ntdll.dll 的其他32位版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ntsym</strong></p></td>
<td align="left"><p>与当前计算机模式匹配的最适合 NT 符号的模块。 在本机模式下进行调试时，此别名与 <strong>$ntnsym</strong>相同。 在非纯模式下进行调试时，调试器会尝试查找与此模式匹配的模块。  (例如，在使用 WOW64 的32位调试期间，此别名与 <strong>$ntwsym</strong>相同。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$CurrentDumpFile</strong></p></td>
<td align="left"><p>调试器加载的最后一个转储文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$CurrentDumpPath</strong></p></td>
<td align="left"><p>调试器加载的最后一个转储文件的目录路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$CurrentDumpArchiveFile</strong></p></td>
<td align="left"><p>) 调试器加载的最后一个转储存档文件 (CAB 文件的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$CurrentDumpArchivePath</strong></p></td>
<td align="left"><p>) 调试器加载的最后一个转储存档文件 (CAB 文件的目录路径。</p></td>
</tr>
</tbody>
</table>

 

自动别名与 [自动伪寄存器](pseudo-register-syntax.md)相似，不同之处在于，可以将带有别名相关标记的自动别名 (如 **$ {}**) ，而不能将伪寄存器用于这些令牌。

### <a name="span-idusing_an_alias_in_the_debugger_command_windowspanspan-idusing_an_alias_in_the_debugger_command_windowspanusing-an-alias-in-the-debugger-command-window"></a><span id="using_an_alias_in_the_debugger_command_window"></span><span id="USING_AN_ALIAS_IN_THE_DEBUGGER_COMMAND_WINDOW"></span>在调试器命令窗口中使用别名

定义别名后，可以在任何命令条目中使用它。 别名将自动替换为等效的别名。 因此，可以将别名用作表达式或宏。

即使别名用引号引起来，别名也会正确扩展。 由于等效的别名可以包含任意数量的引号或分号，因此别名等效项可以代表多个命令。

仅当名称与其他字符之间用空格分隔时，才识别用户命名的别名。 其别名的第一个字符必须以行开头或以空格、分号或引号开头。 其别名的最后一个字符必须以空格结束，后面应跟空格、分号或引号。

**注意**   在 [命令窗口调试器](debugger-command-window.md) 中输入的任何以 "as"、"as"、"ad" 或 "al" 开头的文本都不会接收到别名替换。 此限制可防止别名命令呈现为不可操作。 但是，这种限制也意味着，在行上跟随 **广告** 或 **al** 的命令不会替换其别名。 如果希望将别名替换为以其中一个字符串开头的行，请在别名前面添加一个分号。

 

但是，可以使用 **$ {}** 标记展开用户命名的别名，即使它位于其他文本旁边。 你还可以将此令牌与某些交换机一起使用，以防止别名展开或显示某些与别名相关的值。 有关这些情况的详细信息，请参阅 [**$ {} (别名解释器)**](-------alias-interpreter-.md)。

固定名称的别名会正确地从行内的任何点进行扩展，而不管它在行文本中的嵌入方式如何。

你不能使用只能在 WinDbg (中使用的命令 [**。请打开**](-open--open-source-file-.md)，[**编写 \_ Cmd \_ 他 (写入命令历史记录)**](-write-cmd-hist--write-command-history-.md)、 [**. lsrcpath**](-srcpath---lsrcpath--set-source-path-.md)和 [**. lsrcfix**](-srcfix---lsrcfix--use-source-server-.md)) ，还可以使用一些其他命令 ([**.cls**](-cls--clear-screen-.md)、、 [**wtitle**](-wtitle--set-window-title-.md)、 [**. 远程**](-remote--create-remote-exe-server-.md)、[**内核模式和**](-restart--restart-kernel-connection-.md)用户模式 [**重新启动**](-restart--restart-target-application-.md) [**) 。**](-hh--open-html-help-file-.md)

### <a name="span-idusing_an_alias_in_a_script_filespanspan-idusing_an_alias_in_a_script_filespanusing-an-alias-in-a-script-file"></a><span id="using_an_alias_in_a_script_file"></span><span id="USING_AN_ALIAS_IN_A_SCRIPT_FILE"></span>在脚本文件中使用别名

使用脚本文件中的别名时，必须特别注意，以确保在正确的时间扩展别名。 请看下面的脚本：

```text
.foreach (value {dd 610000 L4})
{
   as /x ${/v:myAlias} value + 1
   .echo value myAlias
}

ad myAlias
```

第一次执行循环时， [**as (设置别名)**](as--as--set-alias-.md) 命令将值分配给 myAlias。 分配给 myAlias 的值为 1 + 610000 (dd 命令) 的第一个输出。 但是，当执行 [**回显 (Echo 注释)**](-echo--echo-comment-.md) 命令时，myAlias 尚未展开，因此，我们将看到文本 "myAlias"，而不是查看610001。

```dbgcmd
0:001> $$>< c:\Script02.txt
00610000 myAlias
00905a4d 0x610001
00000003 0x905a4e
00000004 0x4
0000ffff 0x5
```

问题在于，在输入新的代码块之前，myAlias 不会展开。 循环的下一项是新块，因此 myAlias 扩展到610001。 但它太晚：我们应该在第一次循环时（而不是第二次）看到610001。可以通过在新块中包含 [**回显 (Echo 注释)**](-echo--echo-comment-.md) 命令来解决此问题，如下面的脚本中所示。

```text
.foreach (value {dd 610000 L4}) 
{
   as /x ${/v:myAlias} value + 1
   .block{.echo value myAlias}
}

ad myAlias
```

利用修改后的脚本，我们得到了以下正确的输出。

```dbgcmd
0:001> $$>< c:\Script01.txt
00610000 0x610001
00905a4d 0x905a4e
00000003 0x4
00000004 0x5
0000ffff 0x10000
```

有关详细信息，请参阅 [**block**](-block.md) 和 [**$ {} (别名解释器)**](-------alias-interpreter-.md)。

### <a name="span-idusing_a_foreach_token_in_an_aliasspanspan-idusing_a_foreach_token_in_an_aliasspanspan-idusing_a_foreach_token_in_an_aliasspanusing-a-foreach-token-in-an-alias"></a><span id="Using_a_.foreach_Token_in_an_Alias"></span><span id="using_a_.foreach_token_in_an_alias"></span><span id="USING_A_.FOREACH_TOKEN_IN_AN_ALIAS"></span>在别名中使用 foreach 标记

如果在别名的定义中使用 [**foreach**](-foreach.md) 标记，则必须特别注意，以确保令牌已展开。 请考虑以下命令序列。

```dbgcmd
r $t0 = 5
ad myAlias
.foreach /pS 2 /ps 2 (Token {?@$t0}) {as myAlias Token}
al
```

第一个命令将 **$t 0** 伪寄存器的值设置为5。 第二个命令删除以前可能已分配给 myAlias 的任何值。 第三个命令使用 **？ @ $t 0** 命令的第三个标记，并尝试将该令牌的值分配给 myAlias。 第四个命令列出所有别名及其值。 我们预计 myAlias 的值为5，而值为 "Token"。

```dbgcmd
   Alias            Value  
 -------          ------- 
 myAlias          Token 
```

问题在于， [**as**](as--as--set-alias-.md) 命令位于 [**foreach**](-foreach.md) 循环正文中的行的开头。 当行以 **as** 命令开头时，该行中的别名和标记将不会展开。 如果在 **as** 命令前面加上一个分号或空格，则会扩展已具有值的任何别名或令牌。 在此示例中，myAlias 未展开，因为它还没有值。 标记已展开，因为它的值为5。 下面是在 **as** 命令前面添加分号的相同命令序列。

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

### <a name="span-idrecursive_aliasesspanspan-idrecursive_aliasesspanrecursive-aliases"></a><span id="recursive_aliases"></span><span id="RECURSIVE_ALIASES"></span>递归别名

可以在任何别名的定义中使用固定名称别名。 你还可以在固定名称别名的定义中使用用户命名的别名。 但是，若要在另一个用户命名别名的定义中使用用户命名的别名，则必须在 **as** 或 **as** 命令前面添加一个分号，否则该行上不会出现别名替换。

使用此类型的递归定义时，会在使用每个别名后立即将其转换。 例如，下面的示例显示 **3**，而不是 **7**。

```dbgcmd
0:000> r $.u2=2 
0:000> r $.u1=1+$u2 
0:000> r $.u2=6 
0:000> ? $u1 
Evaluate expression: 3 = 00000003
```

同样，下面的示例显示 **3**，而不是 **7**。

```dbgcmd
0:000> as fred 2 
0:000> r $.u1= 1 + fred 
0:000> as fred 6 
0:000> ? $u1 
Evaluate expression: 3 = 00000003
```

下面的示例也是允许的，并显示 **9**。

```dbgcmd
0:000> r $.u0=2 
0:000> r $.u0=7+$u0 
0:000> ? $u0
Evaluate expression: 9 = 00000009
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

可以使用别名，这样就不必键入长符号名称或复杂符号名称，如下面的示例中所示。

```dbgcmd
0:000> as Short usersrv!NameTooLongToWantToType
0:000> dw Short +8
```

下面的示例与前面的示例类似，但它使用的是固定名称别名。

```dbgcmd
0:000> r $.u0=usersrv!NameTooLongToWantToType
0:000> dw $u0+8
```

对于经常使用的命令，可以使用别名作为宏。 下面的示例递增 **eax** 和 **ebx** 寄存器两次。

```dbgcmd
0:000> as GoUp r eax=eax+1; r ebx=ebx+1
0:000> GoUp
0:000> GoUp
```

下面的示例使用别名来简化命令的键入。

```dbgcmd
0:000> as Cmd "dd esp 14; g"
0:000> bp MyApi Cmd 
```

下面的示例与前面的示例类似，但它使用的是固定名称别名。

```dbgcmd
0:000> r $.u5="dd esp 14; g"
0:000> bp MyApi $u5 
```

上述两个示例都等效于以下命令。

```dbgcmd
0:000> bp MyApi "dd esp 14; g"
```

### <a name="span-idtools_ini_filespanspan-idtools_ini_filespan-toolsini-file"></a><span id="tools_ini_file"></span><span id="TOOLS_INI_FILE"></span> Tools.ini 文件

在 CDB (和 NTSD) 中，可以在 [tools.ini](configuring-tools-ini.md) 文件中预定义固定名称的别名。 若要预定义固定名称别名，请将所需的 **$u** 字段添加到 \[ NTSD \] 条目，如以下示例中所示。

```ini
[NTSD]
$u1:_ntdll!_RtlRaiseException
$u2:"dd esp 14;g"
$u9:$u1 + 42
```

不能在 Tools.ini 文件中设置用户命名的别名。

### <a name="span-idfixed_name_aliases_vs__user_named_aliasesspanspan-idfixed_name_aliases_vs__user_named_aliasesspanfixed-name-aliases-vs-user-named-aliases"></a><span id="fixed_name_aliases_vs__user_named_aliases"></span><span id="FIXED_NAME_ALIASES_VS__USER_NAMED_ALIASES"></span>固定名称别名与 User-Named 别名

用户名别名比固定命名别名更易于使用。 它们的定义语法更简单，可以使用 [**al (列出别名)**](al--list-aliases-.md) 命令来列出它们。

如果在其他文本旁使用，则会替换固定命名的别名。 若要在其他文本旁替换用户命名的别名，请将其放在 [**$ {} (别名解释器)**](-------alias-interpreter-.md) 标记中。

固定名称的别名替换在用户命名的别名替换之前发生。

 

 





