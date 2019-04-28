---
title: bpid
description: Bpid 扩展要求目标计算机上的进程中断到调试器或将用户模式下调试程序附加到目标计算机上的进程的请求。
ms.assetid: 47091651-3b39-4e3d-86cf-a8e95779a025
keywords:
- bpid Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bpid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5bfa8a179571bd4f61ad6b11618eb4def71ecbab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334676"
---
# <a name="bpid"></a>!bpid


**！ Bpid**扩展请求目标计算机上的进程中断到调试器或将用户模式下调试程序附加到目标计算机上的进程的请求。

```dbgcmd
    !bpid [Options] PID 
```

## <a name="span-idddkbpiddbgspanspan-idddkbpiddbgspanparameters"></a><span id="ddk__bpid_dbg"></span><span id="DDK__BPID_DBG"></span>参数


<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *选项*   
此命令的其他活动中的控件。

有效值*选项*显示在下表中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>将新的用户模式下调试程序附加到指定的进程<em>PID</em>。 用户模式下调试程序在目标计算机上运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>在紧靠在用户模式下中断 WinLogon 进程中添加断点发生的指定进程<em>PID</em>。 这允许用户以尝试操作之前验证请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>将请求存储在内存中目标计算机。 然后，在目标系统可以重复请求，但这不是通常只需要。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
指定目标计算机上所需的进程的进程 ID。 如果使用此控制目标计算机上的用户模式调试器*PID*应为目标应用程序，而不是用户模式下调试程序的进程 ID。 (进程 Id 通常列在十进制格式，因为可能需要此操作与前缀**0n**或将其转换为十六进制格式。)

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

在基于 x86、 基于 x64 和基于 Itanium 的目标计算机上支持此扩展命令。

<a name="remarks"></a>备注
-------

此命令将重定向输入和输出从用户模式下调试器到内核调试程序时特别有用。 它会导致用户模式下的目标应用程序，以中断用户模式下调试器，进而从内核调试器请求输入。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

如果在另一种情况下使用此命令，用户模式下处理调用**DbgBreakPoint**。 这通常将直接进入内核调试器中中断。

**-S**选项会引起的中断 WinLogon 之前发生的指定进程中中断。 这是你想要执行 WinLogon 的进程上下文中的调试操作的情况下很有用。 [ **G （转向）** ](g--go-.md)然后可以使用命令转到第二个中断。

请注意的是，此扩展插件可能无法在其中执行的方式：

-   缺少的资源。 **！ Bpid**扩展将线程注入到目标进程中，因此系统必须具有足够的资源来创建线程。 使用 **-a**选项需要更多的系统资源，因为 **！ bpid-a**必须在目标计算机上运行调试器的完整实例。

-   已保留加载程序锁。 这两 **！ bpid**并 **！ bpid-a**需要以使其在目标进程中运行一个线程进入调试器。 如果另一个线程持有加载程序锁，则 **！ bpid**线程都能够运行，可能不会发生中断到调试器。 因此，如果 **！ bpid**时没有足够的用户模式内存可用于目标进程失败，就可以在加载程序锁被保留。

-   缺少的权限。 操作 ！ bpid 扩展需要 WinLogon 创建远程线程并将调试器附加到给定进程的足够权限。

-   Ntsd.exe 没有访问权限。 如果在常见的已知路径中，找不到 ntsd.exe ！ bpid 将无法设置相应的 PID。 请注意默认情况下，使用 Windows Vista 不包含该 ntsd.exe。

 

 





