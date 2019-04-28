---
title: bl（断点列表）
description: Bl 命令将列出有关现有断点的信息。
ms.assetid: 3e7c31d4-5c76-4609-91be-c6b0fc1cb292
keywords:
- bl （断点列表） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bl (Breakpoint List)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6776d96d5fd9690adcb0e835ca991258e2505b2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347871"
---
# <a name="bl-breakpoint-list"></a>bl（断点列表）


**Bl**命令将列出有关现有断点信息。

```dbgcmd
bl [/L] [Breakpoints]
```

## <a name="span-idddkcmdbreakpointlistdbgspanspan-idddkcmdbreakpointlistdbgspanparameters"></a><span id="ddk_cmd_breakpoint_list_dbg"></span><span id="DDK_CMD_BREAKPOINT_LIST_DBG"></span>参数


<span id="________L______"></span><span id="________l______"></span> **/L**   
强制**bl**始终显示断点地址而不是显示源代码文件和行号。

<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span> *断点*   
指定要列出的断点的 ID 号。 如果省略*断点*，调试器会列出所有断点。 可以指定任意数量的断点。 您必须将多个 Id 用空格或逗号。 可以使用连字符指定断点 Id 的范围 （-）。 可以使用星号 (**\\* * *) 以指示所有断点。如果你想要使用[数值表达式](numerical-expression-syntax.md)id，请将其括在方括号中 (*<em>\[\]</em><em>)。如果你想要使用[带有通配符字符的字符串](string-wildcard-syntax.md)若要匹配断点的符号名称，请将其括在引号 (**""</em>*  )。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和如何使用断点、 其他断点的命令和控制断点的方法以及如何从内核调试程序在用户空间中设置断点的示例，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

对于每个断点，该命令显示以下信息：

- 断点 id。 此 ID 是可用于指代更高版本的命令中的断点的十进制数。

- 断点的状态。 状态可以是**e** （启用） 或**d** （禁用）。

- （仅未解析的断点）如果断点是无法解析的会出现字母"u"。 也就是说，断点不匹配任何当前加载的模块中的符号引用。 有关这些断点的信息，请参阅[无法解析断点 (bu 断点)](unresolved-breakpoints---bu-breakpoints-.md)。

- 虚拟地址或符号组成的断点位置的表达式。 如果启用源行号加载**bl**命令显示而不是地址的偏移量的文件和行号信息。 如果无法解析该断点，地址此处省略了，并显示在列表末尾相反。

- （仅适用于数据断点）数据断点被显示类型和大小信息。 类型可以是**e** （执行）， **r** （读/写）， **w** （写入） 或**我**（输入/输出）。 这些类型后面带有块，以字节为单位的大小。 有关这些断点的信息，请参阅[处理器断点 (ba 断点)](processor-breakpoints---ba-breakpoints-.md)。

- 将保留，直到激活断点，则该传递数后跟在括号中传递的初始数量。 有关此类型的断点的详细信息，请参阅的说明*Pass*中的参数[**最佳实践、 bu、 bm （设置断点）**](bp--bu--bm--set-breakpoint-.md)。

- 关联的进程和线程。 如果线程指定为三个星号 ("* *\*\*\\* * *")，此断点不是特定于线程的断点。

- 模块和函数，使用的偏移量，对应于断点地址。 如果无法解析该断点，断点地址此处改为显示，在括号中。 如果是有效的地址上设置断点，但缺少的符号信息，此字段为空。

- 命中此断点时自动执行该命令。 此命令显示在引号中。

如果您不确定使用哪个命令设置现有断点，请使用[ **.bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)若要列出所有断点以及用来创建它们的命令。

下面的示例演示的输出**bl**命令。

示例

```dbgcmd
0:000> bl
 0 e 010049e0     0001 (0001)  0:**** stst!main
```

此输出包含以下信息：

- ID 是的断点**0**。

- 断点状态是**e** （启用）。

- 断点不是未解析 (没有任何**u**输出中)。

- 断点的虚拟地址是**010049e0**。

- 断点处于活动状态上第一次遍历代码和代码具有尚未执行在调试器下。 此信息将由值为 1 (**0001**) 中的"将传递剩余"计数器和值为 1 (**(0001)**) 在初始将传递计数器。

- 此断点不是特定于线程的断点 (* *\*\*\*\\* * *)。

- 上设置断点**主要**中**stst**模块。

 

 





