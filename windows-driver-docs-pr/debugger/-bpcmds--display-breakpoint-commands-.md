---
title: .bpcmds（显示断点命令）
description: Bpcmds 命令显示用于设置每个当前断点的命令。
keywords:
- bpcmds (显示) Windows 调试的断点命令
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bpcmds (Display Breakpoint Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6ad48f4d1c7a389f3f445252ef80ea82cfc1a62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799971"
---
# <a name="bpcmds-display-breakpoint-commands"></a>.bpcmds（显示断点命令）


**Bpcmds** 命令显示用于设置每个当前断点的命令。

```dbgcmd
    .bpcmds
```

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
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用断点的详细信息和示例，请参阅 [使用](using-breakpoints.md)断点和控制断点的方法。

<a name="remarks"></a>备注
-------

如果不清楚是否在某个地址、符号引用或符号处设置了某个特定断点，请使用 **bpcmds** 命令显示用于创建该断点的命令。 用于创建断点的命令确定了其性质：

-   [**Bp (设置断点)**](bp--bu--bm--set-breakpoint-.md)命令在地址处设置断点。

-   [**Bu (设置未解析的断点)**](bp--bu--bm--set-breakpoint-.md)命令在符号引用上设置断点。

-   [**Bm.exe (设置符号断点)**](bp--bu--bm--set-breakpoint-.md)命令在与指定模式匹配的符号上设置断点。 如果包含 **/d** 开关，则它会在 (如 bp) 上的地址中创建零个或多个断点，否则，将在 (如 bu) 上创建零个或多个断点。

-   当 [**Access)**](ba--break-on-access-.md) 命令在某个地址处设置数据断点时，ba (会中断。

**Bpcmds** 的输出反映每个断点的当前特性。 **Bpcmds** 显示的每一行都以用于创建它 (**bp**、 **bu** 或 **ba**) 后跟断点 ID 的命令开始，然后是断点的位置。

如果该断点是通过 **ba** 创建的，则也会显示访问类型和大小。

如果断点是由 **bm.exe** 创建的，而没有 **/d** 开关，则显示的断点类型为 **bu**，后跟 **@！ ""** 中包含的计算符号 标记 (指示它是一个文字符号，而不是数值表达式或寄存器) 。 如果断点是由 **bm.exe** 使用 **/d** 开关创建的，则显示将断点类型指示为 **bp**。

以下是示例：

```dbgcmd
0:000> bp notepad!winmain 

0:000> .bpcmds 
bp0 0x00000001`00003340 ;

0:000> bu myprog!winmain 
breakpoint 0 redefined

0:000> .bpcmds 
bu0 notepad!winmain;

0:000> bu myprog!LoadFile 

0:000> bp myprog!LoadFile+10 

0:000> bm myprog!openf* 
  3: 00421200 @!"myprog!openFile"
  4: 00427800 @!"myprog!openFilter"

0:000> bm /d myprog!closef* 
  5: 00421600 @!"myprog!closeFile"

0:000> ba r2 myprog!LoadFile+2E 

0:000> .bpcmds
bu0 notepad!winmain;
bu1 notepad!LoadFile;
bp2 0x0042cc10 ;
bu3 @!"myprog!openFile";
bu4 @!"myprog!openFilter";
bp5 0x00421600 ;
ba6 r2 0x0042cc2e ;
```

在此示例中，请注意， **bpcmds** 的输出以相关命令开始， ( "bu"、"bp" 或 "ba" ) ，后跟 (没有干预空间) 的断点号。

请注意，由于断点号0最初是使用 **bp** 设置的，然后使用 **bu** 重新定义，因此显示的类型显示为 "bu"。

另请注意，断点3、4和5（由本示例中所示的 **bm.exe** 命令创建）显示为 "最佳类型" 或 "bu" 类型，具体取决于使用 **bm.exe** 时是否包括 **/d** 开关。

 

 





