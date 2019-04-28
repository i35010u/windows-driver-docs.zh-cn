---
title: .context（设置用户模式地址上下文）
description: .Context 命令指定进程的页上的目录将用于用户模式地址上下文，或显示当前的用户模式地址上下文。
ms.assetid: f859b9bf-c05a-44cd-b6f0-8ff4561ddd4e
keywords:
- 设置用户模式地址上下文 (.context) 命令
- 地址，设置用户模式地址上下文 (.context) 命令
- 上下文中，设置用户模式地址上下文 (.context) 命令
- .context （设置用户模式地址上下文） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .context (Set User-Mode Address Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14b6d270f3a75516c1732da48f16b30728c60701
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334620"
---
# <a name="context-set-user-mode-address-context"></a>.context（设置用户模式地址上下文）


**.Context**命令指定进程的页上的目录将用于用户模式地址上下文，或显示当前的用户模式地址上下文。

```dbgsyntax
.context [PageDirectoryBase]
```

## <a name="span-idddkmetasetusermodeaddresscontextdbgspanspan-idddkmetasetusermodeaddresscontextdbgspanparameters"></a><span id="ddk_meta_set_user_mode_address_context_dbg"></span><span id="DDK_META_SET_USER_MODE_ADDRESS_CONTEXT_DBG"></span>参数


<span id="_______PageDirectoryBase______"></span><span id="_______pagedirectorybase______"></span><span id="_______PAGEDIRECTORYBASE______"></span> *PageDirectoryBase*   
指定页所需的流程对目录的基址。 用户模式地址上下文将设置为此页目录中。 如果*PageDirectoryBase*为零，用户模式地址上下文将设置为当前的系统状态的页目录。 如果*PageDirectoryBase*是省略，将显示当前的用户模式地址上下文。

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

有关用户模式地址上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

通常情况下，进行内核调试，仅在可见的用户模式地址空间是与当前进程相关联。

**.Context**命令会指示要使用与指定的页目录的内核调试器*用户模式地址上下文*。 执行此命令后，调试器都可以访问此虚拟地址空间。 此地址空间的页表将用于解释用户模式下的所有内存地址。 这样，您可以读取和写入此内存。

[ **.Process （设置进程上下文）** ](-process--set-process-context-.md)命令具有类似的效果。 但是， **.context**命令的用户模式地址上下文设置为特定页目录中，虽然 **.process**命令集*进程上下文*到特定过程。 X86 处理器，这两个命令具有实质上是相同的效果。 但是，在 Itanium 处理器上，单个进程可能具有多个页目录。 在这种情况下， **.process**命令，功能更强大，因为它将允许对与某进程关联的所有页目录的访问。 请参阅[进程上下文](changing-contexts.md#process-context)的更多详细信息。

如果您正在执行实时调试，则你应发出[ **.cache forcedecodeuser** ](-cache--set-cache-size-.md)命令除了 **.context**命令。 这会强制调试器来查找所需的内存空间的物理地址。 （这可以是较慢，因为这通常意味着必须通过调试缆线传输大量数据。）

如果您打算执行故障转储调试时， [ **.cache** ](-cache--set-cache-size-.md)命令，则不需要。 但是，您不会对虚拟地址空间的任何部分访问权限的用户模式进程的已分页到磁盘发生故障。

下面是一个示例。 使用[ **！ 过程**](-process.md)扩展用于寻找所需的进程基目录：

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS fe5039e0  SessionId: 0  Cid: 0008    Peb: 00000000  ParentCid: 0000
    DirBase: 00030000  ObjectTable: fe529b68  TableSize:  50.
    Image: System

...

PROCESS fe3c0d60  SessionId: 0  Cid: 0208    Peb: 7ffdf000  ParentCid: 00d4
 DirBase: 0011f000  ObjectTable: fe3d0f48  TableSize:  30.
    Image: regsvc.exe
```

现在，使用 **.context**使用此页目录基本命令。

```dbgcmd
kd> .context 0011f000
```

这使您可以检查以各种方式的地址空间。 例如，下面是输出[ **！ peb** ](-peb.md)扩展：

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

 

 





