---
title: .scroll_prefs（控制源滚动首选项）
description: .Scroll_prefs 命令控制到行滚动时显示的源窗口中的源位置。
ms.assetid: 08978751-c4b7-491a-9e1f-de21d74a10a8
keywords:
- .scroll_prefs （滚动首选项控制源） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scroll_prefs (Control Source Scrolling Preferences)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22361c782981011a8fc5a36235973049077594e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339835"
---
# <a name="scrollprefs-control-source-scrolling-preferences"></a>.scroll\_首选项 （控制源滚动首选项）


**.Scroll\_预置**命令控制到行滚动时显示的源窗口中的源位置。

```dbgcmd
.scroll_prefs Before After 
.scroll_prefs 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Before______"></span><span id="_______before______"></span><span id="_______BEFORE______"></span> *之前*   
指定源行数之前的行滚动到应该在源窗口中可见。

<span id="_______After______"></span><span id="_______after______"></span><span id="_______AFTER______"></span> *After*   
指定源行数后，滚动到的行应该在源窗口中可见。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，并能在脚本文件。

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

使用此命令时不带任何参数，将显示当前源滚动首选项。

 

 





