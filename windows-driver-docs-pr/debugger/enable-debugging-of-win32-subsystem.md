---
title: 启用 Win32 子系统调试
description: 启用 Win32 子系统调试
ms.assetid: ea9d1c96-413e-42b7-a0c2-b114aa6de2a6
keywords:
- 启用调试的 Win32 子系统 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e49aa42cdb795a2eea5acd5241c764ad3521560
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323147"
---
# <a name="enable-debugging-of-win32-subsystem"></a>启用 Win32 子系统调试


## <span id="ddk_enable_debugging_of_win32_subsystem_dtools"></span><span id="DDK_ENABLE_DEBUGGING_OF_WIN32_SUBSYSTEM_DTOOLS"></span>


**启用调试 Win32 子系统的**标志将调试的是 NTSD 调试器中的客户端服务器运行时子系统 (csrss.exe)。

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
<td align="left"><p>整个系统的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

NTSD 使用命令将调试进程**ntsd-d-p-1**。

此标志是有效时，才[调试初始命令](debug-initial-command.md)标志 （词典） 或[调试 WinLogon](debug-winlogon.md)还设置了标志 (dwl)。

NTSD 的详细信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)。

 

 





