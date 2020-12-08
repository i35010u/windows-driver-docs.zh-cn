---
title: .process（设置进程上下文）
description: Process 命令指定用于进程上下文的进程。
keywords:
- 设置进程上下文 ( 处理) 命令
- 地址，设置进程上下文 ( 处理) 命令
- 上下文，设置进程上下文 ( 处理) 命令
- 处理、设置进程上下文 ( 处理) 命令
- . 处理 (设置进程上下文) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .process (Set Process Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6276dbe99488d7b095ecd6f84fcb6e7deefeac4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795221"
---
# <a name="process-set-process-context"></a>.process（设置进程上下文）


**Process** 命令指定用于进程上下文的进程。

```dbgcmd
.process [/i] [/p [/r]] [/P] [Process]
```

## <a name="span-idddk_meta_set_process_context_dbgspanspan-idddk_meta_set_process_context_dbgspanparameters"></a><span id="ddk_meta_set_process_context_dbg"></span><span id="DDK_META_SET_PROCESS_CONTEXT_DBG"></span>参数


<span id="________i______"></span><span id="________I______"></span>**/i**   
仅限实时调试;不在本地内核调试期间) 指定要 *invasively* 调试 *进程*。 这种调试意味着目标计算机的操作系统实际使指定的进程处于活动状态。  (没有此选项，则 **process** 命令会改变调试器的输出，但不会影响目标计算机本身。 ) 如果你使用 **/i**，则必须使用 [**g (中转)**](g--go-.md) 命令来执行目标。 几秒钟后，目标将返回到调试器，指定的 *进程* 处于活动状态，并用于处理上下文。

<span id="________p______"></span><span id="________P______"></span>**/p**   
如果使用 **/p** 和 *process* 为非零，则在访问之前，将此进程的所有转换页表项 (pte) 转换为物理地址。 这种转换可能会导致速度降低，因为调试器必须找到此进程使用的所有内存的物理地址。 此外，调试器可能必须在调试电缆之间传输大量的数据。  (此行为与 ) [**缓存 forcedecodeuser**](-cache--set-cache-size-.md)。

如果包含 **/p** 选项，并且 *进程* 为零或省略，则会禁用转换。  (此行为与 ) [**缓存 noforcedecodeptes**](-cache--set-cache-size-.md)。

<span id="________r______"></span><span id="________R______"></span>**/r**   
如果使用 **/r** 和 **/p** 选项，则在设置了进程上下文后重新加载用户模式符号。  (此行为与 [**. reload.sql/user**](-reload--reload-module-.md)相同。 ) 

<span id="________P______"></span><span id="________p______"></span>**/P**   
 (实时调试和完整内存转储仅) 在访问前将所有转换页表项 (Pte) 转换为物理地址，前提是使用 **/p** 并且 *进程* 为非零。 与 **/p** 选项不同， **/p** 选项不仅转换指定进程的所有用户模式和内核模式进程的 pte。 这种转换可能会导致速度降低，因为调试器必须找到所有正在使用的内存的物理地址。 此外，调试器可能必须在调试电缆之间传输大量数据。  (此行为与 ) [**缓存 forcedecodeptes**](-cache--set-cache-size-.md)。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定所需进程的地址。 更准确地 (，此参数将指定此进程) 的 EPROCESS 块地址。 进程上下文设置为此进程。 如果省略了 *process* 或指定零，则进程上下文将重置为当前系统状态的默认进程。  (如果已使用 **/i** 选项设置进程上下文，则必须使用 **/i** 选项重置进程上下文。 ) 

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关进程上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

通常情况下，当您执行内核调试时，唯一可见的用户模式地址空间是与当前进程关联的。

**Process** 命令指示内核调试器使用特定的用户模式进程作为 *处理上下文*。 此使用有多个效果，但最重要的是调试器有权访问此进程的虚拟地址空间。 调试器使用此进程的页表来解释所有用户模式内存地址，以便您可以读取和写入此内存。

[**() 命令 User-Mode 地址上下文设置的上下文**](-context--set-user-mode-address-context-.md)具有类似的效果。 但是， **上下文** 命令将 *用户模式地址上下文* 设置为特定的页面目录，而 **process** 命令将进程上下文设置为特定的进程。 在基于 x86 的处理器上， **. 上下文** 和 **. 进程** 几乎相同。 但在基于 Itanium 的处理器上，一个进程可能有多个页目录。 在这种情况下， **process** 命令的功能更强大，因为它允许访问与进程关联的所有页面目录。 有关过程上下文的详细信息，请参阅 [处理上下文](changing-contexts.md#process-context)。

**注意**   如果要执行实时调试，应使用 **/i** 或 **/p** 参数。 如果没有这些参数之一，将无法正确显示用户模式或会话内存。

 

**/I** 参数激活目标进程。 使用此选项时，必须执行该目标一次，才能使此命令生效。 如果再次执行，则进程上下文将丢失。

**/P** 参数启用 **forcedecodeuser** 设置。  (如果 **forcedecodeuser** 选项已处于活动状态，则无需使用 **/p** 。 ) 进程上下文和 **forcedecodeuser** 状态只有在目标再次执行之后才会继续。

如果要执行故障转储调试，则 **/i** 和 **/p** 选项不可用。 但是，在发生崩溃时，无法访问已分页到磁盘的用户模式进程的虚拟地址空间的任何部分。

如果要使用内核调试器来设置用户空间中的断点，请使用 **/i** 选项将目标切换到正确的进程上下文。

下面的示例演示如何使用 [**！进程**](-process.md) 扩展查找所需进程的 EPROCESS 块的地址。

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS fe5039e0  SessionId: 0  Cid: 0008    Peb: 00000000  ParentCid: 0000
    DirBase: 00030000  ObjectTable: fe529b68  TableSize:  50.
    Image: System

.....

PROCESS fe3c0d60  SessionId: 0  Cid: 0208    Peb: 7ffdf000  ParentCid: 00d4
    DirBase: 0011f000  ObjectTable: fe3d0f48  TableSize:  30.
    Image: regsvc.exe
```

现在，该示例使用带有此进程地址的 **. process** 命令。

```dbgcmd
kd> .process fe3c0d60
Implicit process is now fe3c0d60
```

请注意，此命令会导致不必要的 [**上下文**](-context--set-user-mode-address-context-.md) 命令。 用户模式地址上下文已具有所需的值。

```dbgcmd
kd> .context 
User-mode page directory base is 11f000
```

利用此值，可以通过多种方式检查地址空间。 例如，下面的示例显示 [**！ peb**](-peb.md) 扩展的输出。

```dbgcmd
kd> !peb
PEB at 7FFDF000
    InheritedAddressSpace:    No
    ReadImageFileExecOptions: No
    BeingDebugged:            No
    ImageBaseAddress:         01000000
    Ldr.Initialized: Yes
    Ldr.InInitializationOrderModuleList: 71f40 . 77f68
    Ldr.InLoadOrderModuleList: 71ec0 . 77f58
    Ldr.InMemoryOrderModuleList: 71ec8 . 77f60
        01000000 C:\WINNT\system32\regsvc.exe
        77F80000 C:\WINNT\System32\ntdll.dll
        77DB0000 C:\WINNT\system32\ADVAPI32.dll
        77E80000 C:\WINNT\system32\KERNEL32.DLL
        77D40000 C:\WINNT\system32\RPCRT4.DLL
        77BE0000 C:\WINNT\system32\secur32.dll
    SubSystemData:     0
    ProcessHeap:       70000
    ProcessParameters: 20000
        WindowTitle:  'C:\WINNT\system32\regsvc.exe'
        ImageFile:    'C:\WINNT\system32\regsvc.exe'
        CommandLine:  'C:\WINNT\system32\regsvc.exe'
        DllPath:     'C:\WINNT\system32;.;C:\WINNT\System32;C:\WINNT\system;C:\WINNT;C:\WINNT\system32;C:\WINNT;C:\WINNT\System32\Wbem;C:\PROGRA~1\COMMON~1\AUTODE~1'
        Environment:  0x10000
```

 

 





