---
title: lm（列出已加载的模块）
description: Lm 命令显示指定加载的模块。 输出包括状态和模块的路径。
ms.assetid: ee2283bd-4d3f-4e30-8b32-e286a415bb3a
keywords:
- lm （列出已加载的模块） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lm (List Loaded Modules)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 803d08868069781f43eec4c951818d80fafaec2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383393"
---
# <a name="lm-list-loaded-modules"></a>lm（列出已加载的模块）


**Lm**命令显示指定加载的模块。 输出包括状态和模块的路径。

```dbgcmd
lm Options [a Address] [m Pattern | M Pattern]
```

## <a name="span-idddkcmdlistloadedmodulesdbgspanspan-idddkcmdlistloadedmodulesdbgspanparameters"></a><span id="ddk_cmd_list_loaded_modules_dbg"></span><span id="DDK_CMD_LIST_LOADED_MODULES_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项的任意组合：

<span id="D"></span><span id="d"></span>D  
显示使用的输出[调试器标记语言](debugger-markup-language-commands.md)。

<span id="o"></span><span id="O"></span>o  
显示仅加载的模块。

<span id="l"></span><span id="L"></span>l  
显示仅获取其符号信息已加载的模块。

<span id="v"></span><span id="V"></span>v  
将导致显示详细信息。 显示所包括的符号文件名称、 图像文件名称、 校验和信息、 版本信息、 日期戳，时间戳和是否托管该模块的信息代码 (CLR)。 如果相关标头缺失或分页出未显示此信息。

<span id="u"></span><span id="U"></span>u  
（仅适用于内核模式）仅显示用户模式下符号的信息。

<span id="k"></span><span id="K"></span>k  
（仅适用于内核模式）仅显示内核模式下符号的信息。

<span id="e"></span><span id="E"></span>e  
显示符号时遇到的模块。 这些符号包括有无符号的模块和模块的符号状态为 C，T， \#，M 或导出。 有关这些表示法的详细信息，请参阅[符号状态缩写](symbol-status-abbreviations.md)。

<span id="c"></span><span id="C"></span>c  
显示校验和数据。

<span id="1m"></span><span id="1M"></span>1m  
将输出减少，以便不会包含在内，除非的模块的名称。 如果你使用此选项很有用[ **.foreach** ](-foreach.md)令牌将命令输出传输到另一个命令的输入。

<span id="sm"></span><span id="SM"></span>sm  
对显示模块名称而不是排序的起始地址。

此外，您可以包括以下选项之一。 如果不包含上述任何选项，显示内容包括的符号文件名称。

<span id="i"></span><span id="I"></span>i  
显示的图像文件名称。

<span id="f"></span><span id="F"></span>f  
显示的完整映像路径。 (此路径始终匹配初始加载通知中显示的路径，除非您颁发[ **.reload-s** ](-reload--reload-module-.md)命令。)当使用 f 时，不显示符号的类型信息。

<span id="n"></span><span id="N"></span>n  
显示的图像名称。 当使用 n 时，不显示符号的类型信息。

<span id="p"></span><span id="P"></span>p  
显示映射的映像名称。 当使用 p 时，不显示符号的类型信息。

<span id="t"></span><span id="T"></span>t  
显示的文件时间戳。 当使用 t 时，不显示符号的类型信息。

<span id="_______a_______Address______"></span><span id="_______a_______address______"></span><span id="_______A_______ADDRESS______"></span> *地址*   
指定在此模块中包含的地址。 显示仅包含此地址的模块。 如果地址包含一个表达式，它必须括在括号中。

<span id="_______m_______Pattern______"></span><span id="_______m_______pattern______"></span><span id="_______M_______PATTERN______"></span> m*模式*   
指定模块名称必须与匹配的模式。 模式可以包含各种通配符和说明符。 此信息的语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

**请注意**  在大多数情况下，模块名称是不带文件扩展名的文件名。 例如，如果你想要显示有关 Flpydisk.sys 驱动程序的信息，请使用 lm mflpydisk 命令，不 lm mflpydisk.sys。 在某些情况下，模块名称明显不同于的文件的名称。

 

<span id="_______M_______Pattern______"></span><span id="_______m_______pattern______"></span><span id="_______M_______PATTERN______"></span> m*模式*   
指定映像路径必须与匹配的模式。 模式可以包含各种通配符和说明符。 此信息的语法的详细信息，请参阅[字符串通配符语法](string-wildcard-syntax.md)。

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

**Lm**命令将列出的所有模块和每个模块的符号的状态。

Microsoft Windows Server 2003 和更高版本的 Windows 维护用户模式进程中卸载的模块列表。 用户模式进程或转储文件进行调试时**lm**命令还会显示这些卸载的模块。

此命令显示多个列或字段，每个都有不同的标题。 这些标题的一些具有特定含义：

-   *模块名称*通常是不带文件扩展名的文件名称。 在某些情况下，模块名称明显不同于的文件的名称。

-   符号类型紧随模块名称。 此列未标记。 有关各种状态值的详细信息，请参阅[符号状态缩写](symbol-status-abbreviations.md)。 如果已加载符号，符号文件名称应遵循此列。

-   模块中的第一个地址显示为开始。 模块的结尾显示为结束后第一个地址。 例如，如果开始是"faab4000"是"faab8000"已结束，该模块从扩展 0xFAAB4000 到 0xFAAB7FFF，非独占。

-   **lmv**仅：映像路径列显示了可执行文件，其中包括文件扩展名的名称。 通常情况下，完整路径是包含在用户模式下，但不是在内核模式下。

-   **lmv**仅：加载的符号图像文件值是相同的映像名称，除非 Microsoft CodeView 符号存在。

-   **lmv**仅：通常不使用映射的内存图像文件值。 如果调试器 （例如，小型转储调试期间），映射的图像文件，此值将是映射图像的名称。

下面的代码示例演示**lm**命令与 Windows Server 2003 目标计算机。 此示例中包括的 m 和 s\*选项，因此会显示以"s"开头的唯一模块。

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

以下两个示例演示**lm**命令一次没有任何选项，一次使用 sm 选项。 比较两个示例中的排序顺序。

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

 

 





