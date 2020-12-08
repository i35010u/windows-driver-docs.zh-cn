---
title: .step_filter（设置步骤筛选器）
description: .Step_filter 命令将创建一个函数列表，这些函数将在跟踪) 时跳过 (。
keywords:
- 在 Windows 调试) .step_filter (设置步骤筛选器
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .step_filter (Set Step Filter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9bb43e5bdf5bcdcbe519ebce867e26081a7d3cfd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820387"
---
# <a name="step_filter-set-step-filter"></a>。步骤 \_ 筛选器 (设置步骤筛选器) 


**逐步 \_ 筛选器** 命令创建一个函数列表，该列表将跳过跟踪时)  (逐句通过的函数。 这允许您跟踪代码并仅跳过某些功能。 当一行上有多个函数调用时，还可以在源模式下使用它控制步进。

```dbgcmd
.step_filter "FilterList" 
.step_filter /c 
.step_filter 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_FilterList_"></span><span id="_filterlist_"></span><span id="_FILTERLIST_"></span>**"**<em>FilterList</em>**"**  
指定与要逐过程的函数关联的符号。 *FilterList* 可以包含任意数量的文本模式，用分号分隔。 其中每个模式可能包含各种通配符和说明符;有关详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md) 。 其符号与其中至少一个模式匹配的函数将在跟踪期间逐步进行。 每次使用 **"**<em>FilterList</em>**"** 时，以前的筛选器列表将被丢弃，并完全替换为新列表。

<span id="________c______"></span><span id="________C______"></span>**/c**   
清除筛选器列表。

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

 

<a name="remarks"></a>备注
-------

如果没有任何参数，则 " **步骤 \_ 筛选器** " 将显示当前筛选器列表。

通常情况下，跟踪命令 (例如，使用 "单步执行" 按钮 [**的 "逐**](t--trace-.md) 步骤" 和 " [单步](debug---step-into.md) 执行" 按钮 ![ 屏幕截图 ](images/tbinto.png)) 跟踪功能调用。 但是，如果与所调用函数关联的符号与 *FilterList* 指定的模式相匹配，则该函数将逐步执行，就像在使用步骤命令 (例如， [**p**](p--step-.md)) 已使用过。

如果指令指针位于 "筛选器" 列表中列出的代码内，则任何跟踪或步骤命令都将跳出此函数，如 [**gu**](gu--go-up-.md) 命令或 WinDbg " **跳出** " 按钮。 当然，此筛选器会阻止此类代码在第一个位置进行跟踪，因此仅当更改了筛选器或命中断点时才会发生这种情况。

例如，以下命令将导致跟踪命令跳过所有 CRT 调用：

```dbgcmd
.step_filter "msvcrt!*" 
```

在源模式下进行调试时， **步骤 \_ 筛选器** 命令最有用，因为单个源行上可以有多个函数调用。 [**P**](p--step-.md)和 [**t**](t--trace-.md)命令不能用于分隔这些函数调用。

例如，在下面的行中， [**t**](t--trace-.md) 命令将单步执行 GetTickCount 和 printf，而 [**p**](p--step-.md) 命令将逐过程执行两个函数调用：

```dbgcmd
printf( "%x\n", GetTickCount() );
```

通过 " **步骤 \_ 筛选器** " 命令，您可以筛选出其中的一个调用，同时仍跟踪另一个。

由于这些函数由符号标识，因此单个筛选器可以包含整个模块。 这使你可以筛选出 framework 函数-例如，Microsoft 基础类 (MFC) 或活动模板库 (ATL) 调用。

在程序集模式下进行调试时，每次调用都在不同的行上，因此可以选择逐行执行还是逐行跟踪。 因此，在程序集模式下 **步骤 \_ 筛选器** 并不十分有用。

 

 





