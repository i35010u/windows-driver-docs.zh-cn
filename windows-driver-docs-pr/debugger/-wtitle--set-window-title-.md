---
title: .wtitle（设置窗口标题）
description: Wtitle 命令在 "WinDbg" 窗口或 "NTSD"、"CDB" 或 "KD" 窗口中设置标题。
keywords:
- wtitle (设置窗口标题) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .wtitle (Set Window Title)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1828078d34b260b0fcc4222c4b124614170b369a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794121"
---
# <a name="wtitle-set-window-title"></a>.wtitle（设置窗口标题）


**Wtitle** 命令在 "WinDbg" 窗口或 "NTSD"、"CDB" 或 "KD" 窗口中设置标题。

```dbgcmd
.wtitle Title 
```

## <a name="span-idddk_meta_set_window_title_dbgspanspan-idddk_meta_set_window_title_dbgspanparameters"></a><span id="ddk_meta_set_window_title_dbg"></span><span id="DDK_META_SET_WINDOW_TITLE_DBG"></span>参数


<span id="_______Title______"></span><span id="_______title______"></span><span id="_______TITLE______"></span>*标题*   
要用于窗口的标题。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

无法在脚本文件中使用此命令。

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

对于 CDB、NTSD 或 KD，如果未使用 **wtitle** 命令，则窗口标题与用于启动调试器的命令行相匹配。

对于 WinDbg，如果未使用 **wtitle** ，则主窗口标题将包括目标的名称。 如果调试服务器处于活动状态，则也会显示其连接字符串。 如果有多个调试服务器处于活动状态，则只显示最新的调试服务器。

当使用 **wtitle** 时， *Title* 会替换所有这些信息。 即使稍后启动调试服务器，也不会更改 *标题* 。

不管是否使用此命令，WinDbg 版本号始终显示在窗口标题栏中。

 

 





