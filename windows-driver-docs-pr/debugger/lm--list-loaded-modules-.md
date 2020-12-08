---
title: lm（列出已加载的模块）
description: Lm 命令显示指定的已加载模块。 输出包括模块的状态和路径。
keywords:
- ) Windows 调试的 lm (列表加载的模块
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lm (List Loaded Modules)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b16bf7ec45caaf9d03d9285b286ba595402eff39
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838173"
---
# <a name="lm-list-loaded-modules"></a>lm（列出已加载的模块）


**Lm** 命令显示指定的已加载模块。 输出包括模块的状态和路径。

```dbgcmd
lm Options [a Address] [m Pattern | M Pattern]
```

## <a name="span-idddk_cmd_list_loaded_modules_dbgspanspan-idddk_cmd_list_loaded_modules_dbgspanparameters"></a><span id="ddk_cmd_list_loaded_modules_dbg"></span><span id="DDK_CMD_LIST_LOADED_MODULES_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
下列选项的任意组合：

<span id="D"></span><span id="d"></span>2-d  
使用 [调试器标记语言](debugger-markup-language-commands.md)显示输出。

<span id="o"></span><span id="O"></span>i/o  
仅显示已加载的模块。

<span id="l"></span><span id="L"></span>l  
仅显示已加载符号信息的模块。

<span id="v"></span><span id="V"></span>向量  
使显示更详细。 显示内容包括符号文件名、图像文件名、校验和信息、版本信息、日期戳、时间戳，以及有关模块是否是托管代码 (CLR) 的信息。 如果相关标头缺失或已分页，则不会显示此信息。

<span id="u"></span><span id="U"></span>形  
仅)  (内核模式仅显示用户模式符号信息。

<span id="k"></span><span id="K"></span>温度  
仅)  (内核模式仅显示内核模式符号信息。

<span id="e"></span><span id="E"></span>电邮  
仅显示具有符号问题的模块。 这些符号包括没有符号的模块、符号状态为 C、T、 \# 、M 或导出的模块。 有关这些表示法的详细信息，请参阅 [符号状态缩写](symbol-status-abbreviations.md)。

<span id="c"></span><span id="C"></span>ansi-c  
显示校验和数据。

<span id="1m"></span><span id="1M"></span>万美元  
减少输出，因此不包括模块名称以外的任何内容。 如果使用 [**foreach**](-foreach.md) 标记通过管道将命令输出传递给另一个命令输入，则此选项很有用。

<span id="sm"></span><span id="SM"></span>这些  
按模块名称而不是按起始地址对显示进行排序。

此外，您可以仅包含以下选项之一。 如果不包含这些选项中的任何一个，则显示内容将包含符号文件名。

<span id="i"></span><span id="I"></span>看到  
显示图像文件名称。

<span id="f"></span><span id="F"></span>果  
显示完整的映像路径。  (此路径始终匹配初始加载通知中显示的路径，除非你发出了 [**. 重装-s**](-reload--reload-module-.md) 命令。 ) 使用 f 时，不会显示符号类型信息。

<span id="n"></span><span id="N"></span>北  
显示映像名称。 使用 n 时，不显示符号类型信息。

<span id="p"></span><span id="P"></span>h-p  
显示映射的映像名称。 使用 p 时，不显示符号类型信息。

<span id="t"></span><span id="T"></span>关心  
显示文件时间戳。 使用 t 时，不显示符号类型信息。

<span id="_______a_______Address______"></span><span id="_______a_______address______"></span><span id="_______A_______ADDRESS______"></span>*地址*   
指定包含在此模块中的地址。 仅显示包含此地址的模块。 如果 Address 包含表达式，则必须将其括在括号中。

<span id="_______m_______Pattern______"></span><span id="_______m_______pattern______"></span><span id="_______M_______PATTERN______"></span> m *模式*   
指定模块名称必须匹配的模式。 模式可以包含各种通配符和说明符。 有关此信息的语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。

**注意**   在大多数情况下，模块名称是不带文件扩展名的文件名。 例如，若要显示有关 Flpydisk.sys 驱动程序的信息，请使用 lm mflpydisk 命令，而不是 lm mflpydisk.sys。 在某些情况下，模块名称与文件名明显不同。

 

<span id="_______M_______Pattern______"></span><span id="_______m_______pattern______"></span><span id="_______M_______PATTERN______"></span> M *模式*   
指定图像路径必须匹配的模式。 模式可以包含各种通配符和说明符。 有关此信息的语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

" **Lm** " 命令列出了每个模块的所有模块和符号的状态。

Microsoft Windows Server 2003 和更高版本的 Windows 为用户模式进程保留了一个已卸载的模块列表。 调试用户模式进程或转储文件时， **lm** 命令还会显示这些已卸载的模块。

此命令显示多个列或字段，每个列或字段具有不同的标题。 其中一些标题具有特定的含义：

-   *模块名称* 通常是没有文件扩展名的文件名。 在某些情况下，模块名称与文件名明显不同。

-   符号类型紧跟在模块名称后面。 此列未标记为。 有关各个状态值的详细信息，请参阅 [符号状态缩写](symbol-status-abbreviations.md)。 如果已加载符号，则符号文件名称在此列之后。

-   模块中的第一个地址显示为 "启动"。 模块结束后的第一个地址显示为 end。 例如，如果 start 是 "faab4000"，而 end 是 "faab8000"，则模块从0xFAAB4000 扩展到0xFAAB7FFF （含）。

-   仅限 **lmv** ： "图像路径" 列显示可执行文件的名称，包括文件扩展名。 通常，完整路径包含在用户模式下，而不是在内核模式下。

-   仅限 **lmv** ：除非存在 Microsoft CodeView 符号，否则加载的符号图像文件值与映像名称相同。

-   仅限 **lmv** ：通常不使用映射的内存映像文件值。 如果调试器正在映射图像文件 (例如，在) 小型转储调试期间，此值是映射映像的名称。

下面的代码示例显示了使用 Windows Server 2003 目标计算机的 **lm** 命令。 此示例包含 m 和 s \* 选项，因此只显示以 "s" 开头的模块。

```dbgcmd
kd> lm m s*
start    end        module name
f9f73000 f9f7fd80   sysaudio     (deferred)                 
fa04b000 fa09b400   srv          (deferred)                 
faab7000 faac8500   sr           (deferred)                 
facac000 facbae00   serial       (deferred)                 
fb008000 fb00ba80   serenum      e:\mysymbols\SereEnum.pdb\.......
fb24f000 fb250000   swenum       (deferred)                 

Unloaded modules:
f9f53000 f9f61000   swmidi.sys
fb0ae000 fb0b0000   splitter.sys
fb040000 fb043000   Sfloppy.SYS
```

<a name="examples"></a>示例
--------

以下两个示例显示了一次 **lm** 命令，没有任何选项，一次是 sm 选项。 比较两个示例中的排序顺序。

示例 1：

```dbgcmd
0:000> lm
start    end        module name
01000000 0100d000   stst       (deferred)
77c10000 77c68000   msvcrt     (deferred)
77dd0000 77e6b000   ADVAPI32   (deferred)
77e70000 77f01000   RPCRT4     (deferred)
7c800000 7c8f4000   kernel32   (deferred)
7c900000 7c9b0000   ntdll      (private pdb symbols) c:\db20sym\ntdll.pdb
```

示例 2：

```dbgcmd
0:000> lmsm
start    end        module name
77dd0000 77e6b000   ADVAPI32   (deferred)
7c800000 7c8f4000   kernel32   (deferred)
77c10000 77c68000   msvcrt     (deferred)
7c900000 7c9b0000   ntdll      (private pdb symbols)  c:\db20sym\ntdll.pdb
77e70000 77f01000   RPCRT4     (deferred)
01000000 0100d000   stst       (deferred)
```

 

 





