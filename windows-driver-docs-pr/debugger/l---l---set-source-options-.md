---
title: l+、l-（设置源选项）
description: L + 和 l 命令设置了控制源显示和程序单步执行选项的源行选项。
keywords:
- l +，l- (设置) Windows 调试的源选项
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- l+, l- (Set Source Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 068e9e78dcc15c09a36cfb818ab3db9a35bc93e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806537"
---
# <a name="l-l--set-source-options"></a>l+、l-（设置源选项）

<strong>L +</strong>和 **l** 命令设置了控制源显示和程序单步执行选项的源行选项。

```dbgcmd
l+Option
l-Option
l{+|-}
```

## <a name="span-idddk_cmd_set_source_options_dbgspanspan-idddk_cmd_set_source_options_dbgspanparameters"></a><span id="ddk_cmd_set_source_options_dbg"></span><span id="DDK_CMD_SET_SOURCE_OPTIONS_DBG"></span>参数

<span id="_________or_-"></span><span id="_________OR_-"></span>**+** 或 **-**  
指定指定的选项是打开 (加号 \[ + \]) 还是关闭 (减号 \[ - \]) 。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*选项* 以下选项之一。 选项必须采用小写字母。

<span id="l"></span><span id="L"></span>**l**  
在命令提示符处显示源行号。 可以通过 l-ls 或提示允许-src 禁用源行显示 \_ 。 若要使源行号可见，必须通过这两种机制启用源行显示。

<span id="o"></span><span id="O"></span>**i/o**  
在单步执行代码时，隐藏除源行和行号以外的所有消息 () 。  (**s** 选项还必须处于活动状态，才能使 **o** 选项生效。 ) 

<span id="s"></span><span id="S"></span>**些**  
在命令提示符处显示源行和源行号。

<span id="t"></span><span id="T"></span>**关心**  
启动 [源模式](debugging-in-source-mode.md)。 如果未设置此模式，则调试器处于 [程序集模式下](debugging-in-assembly-mode.md)。

<span id="_"></span>**\** _  
打开或关闭所有选项。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 ### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源调试和相关命令的详细信息，请参阅 [源模式下的调试](debugging-in-source-mode.md)。 有关程序集调试和相关命令的详细信息，请参阅 [程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果省略 _Option *，将显示以前设置的选项。 在这种情况下， **l +** 和 **l** 命令具有相同的效果。 但是， **+** 若要使 **l** 命令正常工作，必须包含加号 () 或减号 ( ) 。

每次发出此命令时，只能包含一个 *选项* 。 如果列出了多个选项，则仅检测到第一个选项。 但是，通过重复发出此命令，你可以打开或关闭所需数量的选项。 换句话说，" **.lst** " 是不起作用的，而 "左 + l"、"+ s"、" **+ t** " 将实现所需的效果。 )  (

当你指定 **s** 选项时，无论你是否指定了 **l** 选项，都将在单步执行代码时显示源行和行号。 除非指定 **s** 选项，否则 **o** 选项不起作用。

源行选项不会生效，除非使用 [**. lines (切换源行支持)**](-lines--toggle-source-line-support-.md) 命令或 [行命令行选项](command-line-options.md)启用行号加载。 默认情况下，如果未使用这些命令，则 WinDbg 会启用源行支持，并且 CDB 会将其关闭。
