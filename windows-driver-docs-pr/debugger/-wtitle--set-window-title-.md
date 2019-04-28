---
title: .wtitle（设置窗口标题）
description: .Wtitle 命令在主窗口中的 WinDbg 或 NTSD、 CDB 或 KD 窗口中设置的标题。
ms.assetid: 9ff74a70-22fd-4bb7-b124-f262a37cfd1f
keywords:
- .wtitle （集窗口标题） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .wtitle (Set Window Title)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a92d75bc91a876439c368309cc660acff4bdb25b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348032"
---
# <a name="wtitle-set-window-title"></a>.wtitle（设置窗口标题）


**.Wtitle**命令在主窗口中的 WinDbg 或 NTSD、 CDB 或 KD 窗口中设置的标题。

```dbgcmd
.wtitle Title 
```

## <a name="span-idddkmetasetwindowtitledbgspanspan-idddkmetasetwindowtitledbgspanparameters"></a><span id="ddk_meta_set_window_title_dbg"></span><span id="DDK_META_SET_WINDOW_TITLE_DBG"></span>参数


<span id="_______Title______"></span><span id="_______title______"></span><span id="_______TITLE______"></span> *Title*   
使用在窗口的标题。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

不能在脚本文件中使用此命令。

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

CDB、 NTSD，或 KD，如果 **.wtitle**不使用命令、 窗口标题与用来启动调试器的命令行相匹配。

有关的 WinDbg 中，如果 **.wtitle**尚未使用，主窗口的标题中包含的目标的名称。 如果调试服务器处于活动状态，以及显示其连接字符串。 如果多个调试服务器处于活动状态，将显示仅最新的密码。

当 **.wtitle**使用，则*标题*替换所有此类信息。 即使更高版本，启动调试服务器*标题*将不会更改。

WinDbg 版本号始终显示在窗口标题栏中，无论是否使用此命令。

 

 





