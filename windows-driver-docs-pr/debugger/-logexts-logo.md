---
title: logexts.logo
description: Logexts.logo 扩展设置，或显示记录器输出选项。
ms.assetid: b094cf4b-1d01-4b84-9032-aa865d680df4
keywords:
- logexts.logo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 686db814fb70116f5c10a04621c4df263aaa058d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521612"
---
# <a name="logextslogo"></a>!logexts.logo


**！ Logexts.logo**扩展插件设置，或显示记录器输出选项。

```dbgcmd
!logexts.logo {e|d} {d|t|v} 
!logexts.logo 
```

## <a name="span-idddklogextslogodbgspanspan-idddklogextslogodbgspanparameters"></a><span id="ddk__logexts_logo_dbg"></span><span id="DDK__LOGEXTS_LOGO_DBG"></span>参数


<span id="_______e_d"></span><span id="_______E_D"></span> **e|d**  
指定是启用 (e) 还是禁用 (d) 所指示的输出类型。

<span id="_______d_t_v"></span><span id="_______D_T_V"></span> **d|t|v**  
指定输出类型。 可使用三种类型的记录器输出： 消息直接发送到调试器 (d)，一个文本文件 (t) 或详细.lgv 文件 (v)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[记录器和日志查看器](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

如果 **！ logexts.logo**使用不带任何参数，则将显示当前的日志记录状态、 输出目录和调试器、 文本文件和详细日志的当前设置：

```dbgcmd
0:000> !logo
Logging currently enabled.

Output directory: MyLogs\LogExts\

Output settings:
  Debugger            Disabled
  Text file           Enabled
  Verbose log         Enabled
```

在上一示例中，输出目录是相对路径，因此它位于相对于在其中启动调试程序的目录。

若要禁用详细日志记录，将使用以下命令：

```dbgcmd
0:000> !logo d v
  Debugger            Disabled
  Text file           Enabled
  Verbose log         Disabled
```

文本文件和.lgv 文件将位于当前的输出目录。 若要读取的.lgv 文件，使用日志查看器。

 

 





