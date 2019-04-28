---
title: .eventlog（显示最近的事件）
description: .Eventlog 命令显示新的 Microsoft Win32 调试事件，如模块加载、 进程创建和终止和线程创建和终止。
ms.assetid: 8075007a-42a2-4973-bb04-cca9a4a1b9b6
keywords:
- .eventlog （显示最新事件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .eventlog (Display Recent Events)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56a217b2d6bd5da76af50c85d8ad134bc23bf859
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334501"
---
# <a name="eventlog-display-recent-events"></a>.eventlog（显示最近的事件）


**.Eventlog**命令将显示新的 Microsoft Win32 调试事件，如模块加载、 进程创建和终止和线程创建和终止。

```dbgcmd
.eventlog 
```

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

**.Eventlog**命令显示了仅 1024年个字符。

下面的示例演示 **.eventlog**命令。

```dbgcmd
0:000> .eventlog
0904.1014: Load module C:\Windows\system32\ADVAPI32.dll at 000007fe`fed80000
0904.1014: Load module C:\Windows\system32\RPCRT4.dll at 000007fe`fe8c0000
0904.1014: Load module C:\Windows\system32\GDI32.dll at 000007fe`fea00000
0904.1014: Load module C:\Windows\system32\USER32.dll at 00000000`76b10000
0904.1014: Load module C:\Windows\system32\msvcrt.dll at 000007fe`fe450000
0904.1014: Load module C:\Windows\system32\COMDLG32.dll at 000007fe`fecf0000
0904.1014: Load module C:\Windows\system32\SHLWAPI.dll at 000007fe`fe1f0000
0904.1014: Load module C:\Windows\WinSxS\amd64_microsoft.windows.common-controls_6595b6414
4ccf1df_6.0.6000.16386_none_1559f1c6f365a7fa\COMCTL32.dll at 000007fe`fbda0000
0904.1014: Load module C:\Windows\system32\SHELL32.dll at 000007fe`fd4a0000
0904.1014: Load module C:\Windows\system32\WINSPOOL.DRV at 000007fe`f77d0000
0904.1014: Load module C:\Windows\system32\ole32.dll at 000007fe`feb10000
0904.1014: Load module C:\Windows\system32\OLEAUT32.dll at 000007fe`feeb0000
Last event: Break instruction exception - code 80000003 (first chance)
```

 

 





