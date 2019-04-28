---
title: .step_filter（设置步骤筛选器）
description: 在跟踪过程中，.step_filter 命令将创建将跳过 （跳过） 的函数的列表。
ms.assetid: 9ce2bed4-fac0-4537-a129-7cb9f1e8725e
keywords:
- .step_filter （设置步骤筛选器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .step_filter (Set Step Filter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a39a8bf4fe882844e31ee9f23d7756017f7e70ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334252"
---
# <a name="stepfilter-set-step-filter"></a>步骤\_筛选器 （设置步骤筛选器）


**步骤\_筛选器**命令将在跟踪过程中创建将跳过 （跳过） 的函数的列表。 这可通过代码跟踪，并跳过只有某些函数。 它还可以控制在一行上有多个函数调用时单步执行到源模式中使用。

```dbgcmd
.step_filter "FilterList" 
.step_filter /c 
.step_filter 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_FilterList_"></span><span id="_filterlist_"></span><span id="_FILTERLIST_"></span>**"**<em>FilterList</em>**"**  
指定与要跳过函数相关联的符号。 *筛选器列表*可以包含任意数量的以分号分隔的文本模式。 每种模式可能包含多个通配符和说明符;请参阅[字符串通配符语法](string-wildcard-syntax.md)有关详细信息。 在跟踪过程中，其符号与至少一个这些模式匹配的函数将被跳过。 每次 **"**<em>筛选器列表</em>**"** 是使用，所有先前的筛选器列表被丢弃，和完全替换为新列表。

<span id="________c______"></span><span id="________C______"></span> **/c**   
清除筛选器列表。

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

 

<a name="remarks"></a>备注
-------

不带任何参数，**步骤\_筛选器**显示当前筛选器列表。

通常情况下，跟踪命令 (例如， [ **t** ](t--trace-.md)或 windbg[调试 | 单步执行](debug---step-into.md)按钮![单步执行按钮的屏幕截图](images/tbinto.png)) 跟踪为函数调用。 但是，如果符号与被调用函数将匹配由指定的模式*筛选器列表*，将于--阶梯函数，就像步骤命令 (例如， [ **p**](p--step-.md)) 已使用。

如果指令指针位于筛选器列表中列出的代码内，任何跟踪或步骤的命令将跳出此函数，如[ **gu** ](gu--go-up-.md)命令或 WinDbg**单步跳出**按钮。 当然，此筛选器将阻止此类代码拥有已跟踪到第一个位置中，因此这仅将会发生如果更改了筛选器或命中断点。

例如，以下命令将会导致跳过所有 CRT 调用跟踪命令：

```dbgcmd
.step_filter "msvcrt!*" 
```

**步骤\_筛选器**时在源模式中进行调试，命令是最有用的因为可以有多个函数将调用一个源行上。 [ **P** ](p--step-.md)并[ **t** ](t--trace-.md)命令不能用于分隔这些函数调用。

例如，在以下行中， [ **t** ](t--trace-.md)命令将单步执行 GetTickCount 和 printf，而[ **p** ](p--step-.md)命令将单步通过这两个函数调用：

```dbgcmd
printf( "%x\n", GetTickCount() );
```

**步骤\_筛选器**命令允许你仍将其他跟踪时筛选出这些调用之一。

函数的符号来标识，因为有单个筛选器可以包括整个模块。 这可以筛选出框架函数-例如，Microsoft 基础类 (MFC) 或活动模板库 (ATL) 调用。

在调试中程序集模式时，每次调用是在不同的行，以便您可以选择是否要单步或跟踪行的行。 因此**步骤\_筛选器**不是在程序集模式下很有用。

 

 





