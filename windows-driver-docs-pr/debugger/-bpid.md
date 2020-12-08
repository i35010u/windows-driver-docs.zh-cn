---
title: bpid
description: Bpid 扩展请求目标计算机上的进程进入调试器或请求将用户模式调试器附加到目标计算机上的进程。
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
ms.openlocfilehash: f03e789304793d72f2535dd1519d53d94d10a4d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799961"
---
# <a name="bpid"></a>!bpid


**！ Bpid** extension 请求目标计算机上的进程进入调试器，或请求将用户模式调试器附加到目标计算机上的进程。

```dbgcmd
    !bpid [Options] PID 
```

## <a name="span-idddk__bpid_dbgspanspan-idddk__bpid_dbgspanparameters"></a><span id="ddk__bpid_dbg"></span><span id="DDK__BPID_DBG"></span>参数


<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*选项*   
控制此命令的其他活动。

下表显示了 *选项* 的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>将新的用户模式调试器附加到 <em>PID</em>指定的进程。 用户模式调试器在目标计算机上运行。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>在由 <em>PID</em>指定的用户模式进程中断之前，在 WinLogon 进程中添加一个断点。 这允许用户在尝试操作之前验证请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>在目标计算机的内存中存储请求。 然后，目标系统可以重复该请求，但这通常是不必要的。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______PID______"></span><span id="_______pid______"></span>*PID*   
指定目标计算机上所需进程的进程 ID。 如果使用此来控制目标计算机上的用户模式调试器， *PID* 应为目标应用程序的进程 ID，而不是用户模式调试器。  (因为进程 Id 通常以十进制格式列出，所以你可能需要将其作为 **0n** 前缀，或将其转换为十六进制格式。 ) 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

基于 x86 的基于 x64 的目标计算机支持此扩展命令。

<a name="remarks"></a>备注
-------

将用户模式调试器的输入和输出重定向到内核调试器时，此命令特别有用。 这会使用户模式目标应用程序进入用户模式调试器，进而请求内核调试器输入。 有关详细信息，请参阅 [控制内核调试器中的 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) 。

如果在其他情况下使用此命令，则用户模式进程将调用 **DbgBreakPoint**。 这通常会直接中断到内核调试器中。

**-S** 选项将在指定进程中发生中断之前，在 WinLogon 中产生中断。 如果要在 WinLogon 的进程上下文中执行调试操作，这会很有用。 然后，可以使用 [**g (中转)**](g--go-.md) 命令移动到第二个断点。

请注意，可以通过以下方式执行此扩展：

-   缺少资源。 **！ Bpid** extension 向目标进程中注入一个线程，因此系统必须具有足够的资源来创建线程。 使用 **-a** 选项以后，还需要更多的系统资源，因为必须在目标计算机上运行完整的调试器实例。 **bpid**

-   已持有加载程序锁。 **！ Bpid** 和 **！ bpid** 都需要一个线程在目标进程中运行，以便使其进入调试器。 如果其他线程正在持有加载程序锁，则 **！ bpid** 线程将无法运行，并且可能不会中断调试器。 因此，如果 **！ bpid** 在有足够的用户模式内存可用于目标进程时失败，则可能会保留加载程序锁。

-   缺少权限。 Bpid 扩展的操作需要权限足以使 WinLogon 创建远程线程，并将调试器附加到给定进程。

-   无权访问 ntsd.exe。 如果在常见的已知路径中找不到 ntsd.exe，！ bpid 将无法设置合适的 PID。 请注意，Windows Vista 默认情况下不包含 ntsd.exe。

 

 





