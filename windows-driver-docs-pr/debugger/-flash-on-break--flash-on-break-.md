---
title: .flash_on_break（中断时刷写）
description: .Flash_on_break 命令指定在最小化 WinDbg 和目标中断时，WinDbg 任务栏项是否闪烁。
keywords:
- .flash_on_break (闪存) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .flash_on_break (Flash on Break)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a9c82e3cf3093658b514a1272cad7d6350a9038d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815533"
---
# <a name="flash_on_break-flash-on-break"></a>。在中断时 \_ \_ (闪烁) 


" **刷新时 \_ 刷新 \_** " 命令指定当最小化 windbg 和目标中断时，windbg 任务栏项是否闪烁。

```dbgcmd
.flash_on_break on 
.flash_on_break off 
.flash_on_break 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______on______"></span><span id="_______ON______"></span>**开启**   
如果将 WinDbg 降到最低并且目标中断到调试器中，则会导致 WinDbg 任务栏项闪烁。 这是 WinDbg 的默认行为。

<span id="_______off______"></span><span id="_______OFF______"></span>**关闭**   
阻止 WinDbg 任务栏项闪烁。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

" **刷新 \_ 时刷新 \_** " 命令仅在 WinDbg 中可用。 无法在脚本文件中使用此命令。

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

 

<a name="remarks"></a>备注
-------

如果在没有参数的情况下使用 "不使用 **flash \_ \_** " 命令，调试器将显示当前的 flash 设置。

 

 





