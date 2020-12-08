---
title: .suspend_ui（挂起 WinDbg 接口）
description: .Suspend_ui 命令挂起对 WinDbg 调试信息窗口的刷新。
keywords:
- .suspend_ui (挂起 WinDbg 接口) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .suspend_ui (Suspend WinDbg Interface)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 390866593295da20a1d84ec23f64714e485354a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824391"
---
# <a name="suspend_ui-suspend-windbg-interface"></a>. 暂停 \_ ui (挂起 WinDbg 接口) 


**挂起 \_ ui** 命令挂起对 WinDbg 调试信息窗口的刷新。

```dbgcmd
.suspend_ui 0 
.suspend_ui 1 
.suspend_ui 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______0______"></span>**0**   
挂起对 WinDbg 调试信息窗口的刷新。

<span id="_______1______"></span>**1**   
启用对 WinDbg 调试信息窗口的刷新。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，不能在脚本文件中使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
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

有关调试信息窗口的信息，请参阅 [使用调试信息窗口](using-debugging-information-windows.md)。

<a name="remarks"></a>备注
-------

如果没有任何参数，则 " **挂起 \_ ui** " 将显示调试信息窗口当前是否处于挂起状态。

默认情况下，每次显示的信息发生更改时，都会刷新 "调试信息" 窗口。

暂停这些 windows 的刷新可以在一系列快速操作期间加快 WinDbg 的运行，例如，当快速连续跟踪或单步执行时。

 

 





