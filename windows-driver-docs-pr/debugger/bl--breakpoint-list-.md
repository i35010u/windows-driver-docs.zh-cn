---
title: bl（断点列表）
description: Bl 命令列出有关现有断点的信息。
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
ms.openlocfilehash: dd69b601b4c4b80202c8c1a900767f53c4ffe51f
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284923"
---
# <a name="bl-breakpoint-list"></a>bl（断点列表）


**Bl**命令列出有关现有断点的信息。

```dbgcmd
bl [/L] [Breakpoints]
```

## <a name="span-idddk_cmd_breakpoint_list_dbgspanspan-idddk_cmd_breakpoint_list_dbgspanparameters"></a><span id="ddk_cmd_breakpoint_list_dbg"></span><span id="DDK_CMD_BREAKPOINT_LIST_DBG"></span>Parameters


<span id="________L______"></span><span id="________l______"></span> **/L**   
强制**bl**始终显示断点地址，而不是显示源文件和行号。

<span id="_______Breakpoints______"></span><span id="_______breakpoints______"></span><span id="_______BREAKPOINTS______"></span>*断点*   
指定要列出的断点的 ID 号。 如果省略*断点*，调试器会列出所有断点。 可以指定任意数量的断点。 必须用空格或逗号分隔多个 Id。 您可以通过使用连字符（-）指定断点 Id 的范围。 可以使用星号（\*）来指示所有断点。 如果要对 ID 使用[数值表达式](numerical-expression-syntax.md)，请将其括在括号中（\[\]）。 如果要使用[带有通配符的字符串](string-wildcard-syntax.md)来匹配断点的符号名称，请将其括在引号中（\"\"）。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用断点、其他断点命令和控制断点的方法以及如何在用户空间中从内核调试器设置断点的详细信息，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

对于每个断点，命令会显示以下信息：

- 断点 ID。 此 ID 是一个十进制数，可用于在后面的命令中引用该断点。

- 断点状态。 状态可以为**e** （enabled）或**d** （disabled）。

- （仅限未解析的断点）如果断点未解析，则会出现字母 "u"。 也就是说，该断点与任何当前加载的模块中的符号引用都不匹配。 有关这些断点的信息，请参阅[未解析的断点（Bu 断点）](unresolved-breakpoints---bu-breakpoints-.md)。

- 构成断点位置的虚拟地址或符号表达式。 如果启用了源行号加载，则**bl**命令将显示文件和行号信息而不是地址偏移量。 如果未解析断点，则会在此处省略地址并显示在列表的末尾。

- （仅数据断点）显示数据断点的类型和大小信息。 类型可以是**e** （execute）、 **r** （读/写）、 **w** （write）或**i** （输入/输出）。 这些类型后跟块的大小（以字节为单位）。 有关这些断点的信息，请参阅[处理器断点（Ba 断点）](processor-breakpoints---ba-breakpoints-.md)。

- 在断点被激活之前剩余的传递数，后跟用括号括起的初始数目。 有关此类*断点的详细*信息，请参阅[**bp、bu、Bm.exe （设置断点）** ](bp--bu--bm--set-breakpoint-.md)中 pass 参数的描述。

- 关联的进程和线程。 如果将线程指定为三个星号（\*\*\*），则此断点不是线程特定的断点。

- 与断点地址相对应的模块和函数，具有偏移量。 如果未解析断点，则在此处显示断点地址，而不是括号。 如果对有效地址设置了断点，但缺少符号信息，则此字段为空。

- 命中此断点时自动执行的命令。 此命令显示在引号中。

如果您不确定用于设置现有断点的命令，请使用[ **. bpcmds （显示断点命令）** ](-bpcmds--display-breakpoint-commands-.md)列出所有断点以及用于创建断点的命令。

下面的示例显示了**bl**命令的输出。

示例

```dbgcmd
0:000> bl
 0 e 010049e0     0001 (0001)  0:**** stst!main
```

此输出包含以下信息：

- 断点 ID 为**0**。

- 断点状态为**e** （已启用）。

- 断点不可解析（输出中没有**u** ）。

- 断点的虚拟地址为**010049e0**。

- 在第一次通过代码时，断点处于活动状态，并且尚未在调试器下执行代码。 此信息由 "通过剩余" 计数器中的值1（**0001**）表示，初始传递计数器中的值为1（**0001）** 。

- 此断点不是线程特定的断点（\*\*\*）。

- 在**stst**模块中的**main**上设置断点。

 

 





