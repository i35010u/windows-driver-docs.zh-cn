---
title: logexts 徽标
description: Logexts 扩展会设置或显示记录器输出选项。
keywords:
- logexts Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed838eccbcb77f2140dcc2b7db86c00d9fbe7b57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829777"
---
# <a name="logextslogo"></a>!logexts.logo


**！ Logexts** 扩展设置或显示记录器输出选项。

```dbgcmd
!logexts.logo {e|d} {d|t|v} 
!logexts.logo 
```

## <a name="span-idddk__logexts_logo_dbgspanspan-idddk__logexts_logo_dbgspanparameters"></a><span id="ddk__logexts_logo_dbg"></span><span id="DDK__LOGEXTS_LOGO_DBG"></span>参数


<span id="_______e_d"></span><span id="_______E_D"></span>**e | d**  
指定是启用 (e) 还是禁用 (d) 指定的输出类型。

<span id="_______d_t_v"></span><span id="_______D_T_V"></span>**d | t | v**  
指定输出类型。 可以使用三种类型的记录器输出：直接发送到调试器的消息 (d) ，文本文件 (t) ，或 (v) 的 lgv 文件。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [记录器和 LogViewer](logger-and-logviewer.md)。

<a name="remarks"></a>备注
-------

如果在没有任何参数的情况下使用 **！ logexts** ，则会显示当前日志记录状态、输出目录和调试器、文本文件和详细日志的当前设置：

```dbgcmd
0:000> !logo
Logging currently enabled.

Output directory: MyLogs\LogExts\

Output settings:
  Debugger            Disabled
  Text file           Enabled
  Verbose log         Enabled
```

在上面的示例中，输出目录是相对路径，因此它相对于启动调试器的目录进行定位。

若要禁用详细日志记录，请使用以下命令：

```dbgcmd
0:000> !logo d v
  Debugger            Disabled
  Text file           Enabled
  Verbose log         Disabled
```

文本文件和 lgv 文件将放在当前的输出目录中。 若要读取 lgv 文件，请使用 LogViewer。

 

 





