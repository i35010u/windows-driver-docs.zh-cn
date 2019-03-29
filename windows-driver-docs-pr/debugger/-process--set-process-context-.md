---
title: .process（设置进程上下文）
description: .Process 命令指定哪个进程用于处理上下文。
ms.assetid: f454faef-bc28-43f1-b511-bcee0c12fc24
keywords:
- 设置进程上下文 (.process) 命令
- 地址，设置过程上下文 (.process) 命令
- 上下文中，设置过程上下文 (.process) 命令
- 进程中，设置过程上下文 (.process) 命令
- .process （设置进程上下文） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .process (Set Process Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ad91066a0d80f68a64ee2fe213e30bbda8acea4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577427"
---
# <a name="process-set-process-context"></a>.process（设置进程上下文）


**.Process**命令指定哪个进程用于处理上下文。

```dbgcmd
.process [/i] [/p [/r]] [/P] [Process]
```

## <a name="span-idddkmetasetprocesscontextdbgspanspan-idddkmetasetprocesscontextdbgspanparameters"></a><span id="ddk_meta_set_process_context_dbg"></span><span id="DDK_META_SET_PROCESS_CONTEXT_DBG"></span>参数


<span id="________i______"></span><span id="________I______"></span> **/i**   
实时调试仅;不在本地内核调试） 过程中指定*进程*是要调试*invasively*。 调试此类表示，目标计算机的操作系统实际上使指定的进程处于活动状态。 (如果不使用此选项， **.process**命令更改调试器的输出，但不会影响目标计算机本身。)如果您使用 **/i**，则必须使用[ **g （转向）** ](g--go-.md)命令来执行的目标。 几秒钟后，目标返回在中中断到调试器，并指定*进程*处于活动状态且用于进程上下文。

<span id="________p______"></span><span id="________P______"></span> **/p**   
将所有过渡页表项 (Pte) 都转换到物理地址之前访问权限，此过程中，如果您使用 **/p**并*进程*为非零值。 这种转换可能导致速度变慢，因为调试器必须找到的所有内存，此过程使用的物理地址。 此外，调试器可能需要调试电缆上的传输大量数据。 (此行为是相同[ **.cache forcedecodeuser**](-cache--set-cache-size-.md)。)

如果包括 **/p**选项和*进程*为零或省略，转换已禁用。 (此行为是相同[ **.cache noforcedecodeptes**](-cache--set-cache-size-.md)。)

<span id="________r______"></span><span id="________R______"></span> **/r**   
将重新加载用户模式符号后进程上下文已设置，如果您使用 **/r**并 **/p**选项。 (此行为是相同[ **.reload /user**](-reload--reload-module-.md)。)

<span id="________P______"></span><span id="________p______"></span> **/P**   
（实时调试和仅完全内存转储）转换所有过渡页表项 (Pte) 到物理地址之前访问权限，如果您使用 **/P**并*进程*为非零值。 与不同 **/p**选项， **/P**选项将为所有用户模式和内核模式进程，而不仅仅是指定进程 Pte。 这种转换可能导致速度变慢，因为调试器必须找到物理地址中使用的所有内存。 此外，调试器可能需要调试电缆上的传输大量数据。 (此行为是相同[ **.cache forcedecodeptes**](-cache--set-cache-size-.md)。)

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定所需的进程的地址。 （更准确地说，此参数指定用于此过程的 EPROCESS 块的地址）。 进程上下文设置为此过程。 如果省略*进程*指定零，或进程上下文重置为当前的系统状态的默认过程。 (如果您使用了 **/i**选项来设置进程上下文中，必须使用 **/i**重置进程上下文的选项。)

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关进程上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

通常情况下，进行内核调试，仅在可见的用户模式地址空间是与当前进程相关联。

**.Process**命令会指示要使用与特定的用户模式进程的内核调试器*进程上下文*。 这种用法具有多个效果，但最重要的是调试器有权访问此进程的虚拟地址空间。 调试器使用此过程的页表来解释所有用户模式内存地址，因此你可以读取和写入此内存。

[ **.Context （设置用户模式地址上下文）** ](-context--set-user-mode-address-context-.md)命令具有类似的效果。 但是， **.context**命令集*用户模式地址上下文*到特定页目录中，而 **.process**命令设置为特定的进程上下文过程。 在基于 x86 的处理器上， **.context**并 **.process**具有几乎相同的效果。 但是，在基于 Itanium 处理器上，单个进程可能会有多个页目录。 在此情况下， **.process**命令是更强大，因为它可以使所有与进程关联的页目录访问权限。 有关进程上下文的详细信息，请参阅[进程上下文](changing-contexts.md#process-context)。

**请注意**  如果您正在执行实时调试，则应使用 **/i**或 **/p**参数。 而无需其中一个参数，不能正确显示用户模式或会话内存。

 

**/I**参数激活目标进程。 使用此选项时，必须执行一次此命令才会生效的目标。 如果再次执行进程上下文会丢失。

**/P**参数启用**forcedecodeuser**设置。 (无需使用 **/p**如果**forcedecodeuser**选项已处于活动状态。)进程上下文和**forcedecodeuser**状态保持仅之前目标会再次执行。

如果您正在执行崩溃转储调试时， **/i**并 **/p**选项将不可用。 但是，不能访问任何部分崩溃发生的已分页到磁盘的用户模式进程的虚拟地址空间。

如果想要使用内核调试程序要在用户空间中设置断点，请使用 **/i**选项切换到正确的进程上下文的目标。

下面的示例演示如何使用[ **！ 过程**](-process.md)扩展来查找所需的进程的 EPROCESS 块的地址。

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

现在，该示例使用 **.process**命令与此进程的地址。

```dbgcmd
kd> .process fe3c0d60
Implicit process is now fe3c0d60
```

请注意，此命令让[ **.context** ](-context--set-user-mode-address-context-.md)不必要的命令。 用户模式地址上下文已具有所需的值。

```dbgcmd
kd> .context 
User-mode page directory base is 11f000
```

此值，可以检查以各种方式的地址空间。 例如，下面的示例显示的输出[ **！ peb** ](-peb.md)扩展。

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

 

 





