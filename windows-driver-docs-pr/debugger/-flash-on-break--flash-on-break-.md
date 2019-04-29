---
title: .flash_on_break（中断时刷写）
description: .Flash_on_break 命令指定 WinDbg 任务栏条目闪烁 WinDbg 最小化和中断目标时。
ms.assetid: b2f0a8c5-5b32-44f4-9546-c75859476ce0
keywords:
- .flash_on_break (flash 上中断) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .flash_on_break (Flash on Break)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b735bbfeb806737ec1a39a8518e8ca5f357dc51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336670"
---
# <a name="flashonbreak-flash-on-break"></a>.flash\_上\_中断 (Flash 上中断)


**.Flash\_上\_中断**命令指定 WinDbg 任务栏条目闪烁 WinDbg 最小化和中断目标时。

```dbgcmd
.flash_on_break on 
.flash_on_break off 
.flash_on_break 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______on______"></span><span id="_______ON______"></span> **on**   
使 WinDbg 任务栏条目闪烁，如果 WinDbg 最小化，并且目标进入调试器。 这是 WinDbg 的默认行为。

<span id="_______off______"></span><span id="_______OFF______"></span> **off**   
防止闪烁 WinDbg 任务栏条目。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**.Flash\_上\_中断**命令是仅在 WinDbg 中可用。 不能在脚本文件中使用此命令。

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

如果您使用 **.flash\_上\_中断**命令不带参数，则调试器会显示闪存的当前设置。

 

 





