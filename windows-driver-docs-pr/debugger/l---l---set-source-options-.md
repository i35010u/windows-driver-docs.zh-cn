---
title: l+、l-（设置源选项）
description: L + 和 l 命令设置了控制源显示和程序单步执行选项的源行选项。
ms.assetid: 7b169af0-e799-47eb-b197-c4408a755702
keywords:
- l +，l-（设置源选项） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- l+, l- (Set Source Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 040fa89e792f597d10da46d4668f6460079dc21b
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038094"
---
# <a name="l-l--set-source-options"></a>l+、l-（设置源选项）

<strong>L +</strong>和**l**命令设置了控制源显示和程序单步执行选项的源行选项。

```dbgcmd
l+Option
l-Option
l{+|-}
```

## <a name="span-idddk_cmd_set_source_options_dbgspanspan-idddk_cmd_set_source_options_dbgspanparameters"></a><span id="ddk_cmd_set_source_options_dbg"></span><span id="DDK_CMD_SET_SOURCE_OPTIONS_DBG"></span>Parameters

<span id="_________or_-"></span><span id="_________OR_-"></span> **+** 或 **-**  
指定是否启用给定选项（加号 \[ @ no__t-1 @ no__t-2）或关闭（减号 \[ @ no__t @ no__t）。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*选项*以下选项之一。 选项必须采用小写字母。

<span id="l"></span><span id="L"></span>**l**  
在命令提示符处显示源行号。 可以通过 l-ls 或. prompt @ no__t-0allow-src 禁用源行显示。 若要使源行号可见，必须通过这两种机制启用源行显示。

<span id="o"></span><span id="O"></span>**i/o**  
单步执行代码时，隐藏所有消息（源行和行号除外）。 （ **S**选项必须也处于活动状态，以使**o**选项有任何效果。）

<span id="s"></span><span id="S"></span>**些**  
在命令提示符处显示源行和源行号。

<span id="t"></span><span id="T"></span>**关心**  
启动[源模式](debugging-in-source-mode.md)。 如果未设置此模式，则调试器处于[程序集模式下](debugging-in-assembly-mode.md)。

<span id="_"></span>**\***  
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
<td align="left"><p><strong>适用</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 ### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关源调试和相关命令的详细信息，请参阅[源模式下的调试](debugging-in-source-mode.md)。 有关程序集调试和相关命令的详细信息，请参阅[程序集模式下的调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果省略*选项*，则显示以前设置的选项。 在这种情况下， **l +** 和**l**命令具有相同的效果。 但是，必须包含加号（ **+** ）或减号（-），才能使用**l**命令。

每次发出此命令时，只能包含一个*选项*。 如果列出了多个选项，则仅检测到第一个选项。 但是，通过重复发出此命令，你可以打开或关闭所需数量的选项。 （换句话说，"+" **.lst**不起作用，而 "+ l"、"+ s"、" **+ t** " 将实现所需的效果。）

当你指定**s**选项时，无论你是否指定了**l**选项，都将在单步执行代码时显示源行和行号。 除非指定**s**选项，否则**o**选项不起作用。

源行选项不会生效，除非通过使用[**lines （切换源代码行支持）** ](-lines--toggle-source-line-support-.md)命令或[行命令行选项](command-line-options.md)启用行号加载。 默认情况下，如果未使用这些命令，则 WinDbg 会启用源行支持，并且 CDB 会将其关闭。
