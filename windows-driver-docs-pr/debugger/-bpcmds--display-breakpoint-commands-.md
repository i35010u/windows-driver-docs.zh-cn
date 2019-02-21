---
title: .bpcmds （显示断点命令）
description: .Bpcmds 命令显示了用于设置每个当前断点的命令。
ms.assetid: 96c13c54-8d85-414c-9775-a0373459dc7a
keywords:
- .bpcmds （显示断点命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bpcmds (Display Breakpoint Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d77eebdf2b11279981f51560ab849f9ae985f4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554099"
---
# <a name="bpcmds-display-breakpoint-commands"></a>.bpcmds （显示断点命令）


**.Bpcmds**命令显示了用于设置每个当前断点的命令。

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和如何使用断点、 其他断点的命令和控制断点的方法的示例，请参阅[使用断点](using-breakpoints.md)。

<a name="remarks"></a>备注
-------

如果不清楚一个地址、 的符号的引用，或一个符号是否设置了特定断点，使用 **.bpcmds**命令显示了哪个断点命令用于创建它。 用于创建断点的命令确定它的性质：

-   [**最佳实践 （设置断点）** ](bp--bu--bm--set-breakpoint-.md)命令的地址处设置断点。

-   [ **Bu （设置无法解析断点）** ](bp--bu--bm--set-breakpoint-.md)命令的符号引用上设置断点。

-   [ **Bm （设置符号断点）** ](bp--bu--bm--set-breakpoint-.md)命令与指定的模式匹配的符号上设置断点。 如果 **/d**包含开关，其地址 （如 bp) 上创建零个或多个断点，否则上 （如 bu 锁） 的符号引用创建零个或多个断点。

-   [ **Ba （中断的访问权限）** ](ba--break-on-access-.md)命令设置数据断点所在的地址。

输出 **.bpcmds**反映每个断点的当前特性。 每一行 **.bpcmds**显示开头来创建它所使用的命令 (**bp**， **bu**，或**ba**) 的断点 ID 后, 跟和然后该断点的位置。

如果通过创建断点**ba**，访问类型和大小也会显示。

如果通过创建断点**bm**而无需 **/d**开关，显示表示形式的断点类型**bu**后, 跟括起来计算符号 **@!""** （这表明它是一种文字符号并不是数值表达式或注册） 的标记。 如果通过创建断点**bm**与 **/d**开关，显示表示形式的断点类型**bp**。

下面是一个示例：

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

在此示例中，可以看到的输出 **.bpcmds**开头跟断点数 （与没有干预空格） 的相关命令 （"bu"、"最佳实践"或"ba"）。

请注意，因为最初使用设置断点号 0 **bp**，然后重定义使用和**bu**，屏幕将显示"bu"作为其类型。

另请注意 3、 4 和 5，创建的该断点**bm**此示例中所示的命令显示为任一类型"最佳实践"或键入"bu"，具体取决于是否 **/d**时切换已包括在内**bm**使用。

 

 





