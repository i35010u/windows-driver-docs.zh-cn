---
title: l+、l-（设置源选项）
description: L + 和 l 命令将源设置行选项，控制源显示和程序单步执行选项。
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
ms.openlocfilehash: b2afa93e9891c9e07c03c7af905a7f72064a19ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575322"
---
# <a name="l-l--set-source-options"></a>l+、l-（设置源选项）


<strong>L +</strong>并**l-** 命令将源设置行选项，控制源显示和程序单步执行选项。

```dbgcmd
l+Option 
l-Option 
l{+|-} 
```

## <a name="span-idddkcmdsetsourceoptionsdbgspanspan-idddkcmdsetsourceoptionsdbgspanparameters"></a><span id="ddk_cmd_set_source_options_dbg"></span><span id="DDK_CMD_SET_SOURCE_OPTIONS_DBG"></span>参数


<span id="_________or_-"></span><span id="_________OR_-"></span> **+** 或 **-**  
指定给定的选项是否处于开启 (加号\[ + \]) 或已关闭 (负号\[ - \])。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *选项*   
以下选项之一。 选项必须为小写字母。

<span id="l"></span><span id="L"></span>**l**  
在命令提示符下显示源行号。 您可以禁用源代码行显示通过 l ls 或.prompt\_允许-src。若要使源行可见，则必须启用源行号显示通过这两种机制。

<span id="o"></span><span id="O"></span>**o**  
隐藏所有消息 （而不是源行和行号） 时逐句通过代码。 ( **S**选项还必须为 active **o**选项产生任何作用。)

<span id="s"></span><span id="S"></span>**s**  
在命令提示符下显示源行和源行号。

<span id="t"></span><span id="T"></span>**t**  
启动[源模式](debugging-in-source-mode.md)。 如果未设置此模式下，调试器处于[程序集模式](debugging-in-assembly-mode.md)。

<span id="_"></span>**\\***  
打开或关闭所有选项。

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

有关源调试相关的命令的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。 调试和相关命令，请参阅有关程序集的详细信息[在程序集模式下调试](debugging-in-assembly-mode.md)。

<a name="remarks"></a>备注
-------

如果省略*选项*，则以前显示的 set 选项。 在这种情况下， **l +** 并**l-** 命令具有相同的效果。 但是，必须包括一个加号 (**+**) 或减号 （-） 用于**l**命令能够起作用。

您可只包含一个*选项*每当时，发出此命令。 如果列出多个选项，则只有第一个选项是检测到。 但是，通过反复发出此命令，可以打开或关闭所需的任意多个选项。 (即， **l + lst**不起作用，但**l + l; l + s; l + t** does 实现您想要的效果。)

当指定**s**时单步执行代码，无论是否指定，将显示选项、 源代码行和行号**l**选项。 **O**选项没有任何影响，除非指定，否则**s**选项。

源行选项才会生效，除非您启用使用加载的行号[ **.lines （切换源行支持）** ](-lines--toggle-source-line-support-.md)命令或[-行命令行选项](command-line-options.md). 默认情况下，如果没有使用这些命令，WinDbg 开启源行支持和 CDB 会将其关闭。

 

 





