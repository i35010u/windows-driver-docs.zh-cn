---
title: 启用 Win32 子系统调试
description: 启用 Win32 子系统调试
keywords:
- '启用 Win32 子系统 (全局标志的调试) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 917ce2a77e8330de22ddd4a46481041d5871364f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834763"
---
# <a name="enable-debugging-of-win32-subsystem"></a>启用 Win32 子系统调试


## <span id="ddk_enable_debugging_of_win32_subsystem_dtools"></span><span id="DDK_ENABLE_DEBUGGING_OF_WIN32_SUBSYSTEM_DTOOLS"></span>


**启用 Win32 子系统标记调试** 在 NTSD 调试器中调试客户端服务器运行时子系统 ( # A0) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>d32</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x20000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_ENABLE_CSRDEBUG</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

NTSD 使用命令 **ntsd-d-p-1** 调试进程。

仅当 [调试初始命令](debug-initial-command.md) 标志 (.dic) 或 [调试 WinLogon](debug-winlogon.md) 标志 (dwl) 也设置为 "调试" 时，此标志才有效。

有关 NTSD 的详细信息，请参阅 [使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)。

 

 





