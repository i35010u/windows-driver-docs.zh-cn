---
title: .context（设置用户模式地址上下文）
description: Context 命令指定进程的哪个页面目录将用于用户模式地址上下文，或显示当前用户模式地址上下文。
ms.assetid: f859b9bf-c05a-44cd-b6f0-8ff4561ddd4e
keywords:
- 设置用户模式地址上下文 ( 上下文) 命令
- 地址，设置用户模式地址上下文 ( 上下文) 命令
- 上下文，设置用户模式地址上下文 ( 上下文) 命令
- 。上下文 (设置用户模式地址上下文) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .context (Set User-Mode Address Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09dc571decf5b45670718121564f052976c024c1
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148470"
---
# <a name="context-set-user-mode-address-context"></a>.context（设置用户模式地址上下文）


**Context**命令指定进程的哪个页面目录将用于用户模式地址上下文，或显示当前用户模式地址上下文。

```dbgsyntax
.context [PageDirectoryBase]
```

## <a name="span-idddk_meta_set_user_mode_address_context_dbgspanspan-idddk_meta_set_user_mode_address_context_dbgspanparameters"></a><span id="ddk_meta_set_user_mode_address_context_dbg"></span><span id="DDK_META_SET_USER_MODE_ADDRESS_CONTEXT_DBG"></span>参数


<span id="_______PageDirectoryBase______"></span><span id="_______pagedirectorybase______"></span><span id="_______PAGEDIRECTORYBASE______"></span>*PageDirectoryBase*   
指定所需进程的页面目录的基址。 用户模式地址上下文将设置为此页目录。 如果*PageDirectoryBase*为零，则用户模式地址上下文将设置为当前系统状态的页面目录。 如果省略*PageDirectoryBase* ，则显示当前用户模式地址上下文。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关用户模式地址上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

通常情况下，在进行内核调试时，只有一个可见的用户模式地址空间是与当前进程关联的。

**Context**命令指示内核调试器使用指定的页面目录作为*用户模式地址上下文*。 执行此命令后，调试器将有权访问此虚拟地址空间。 此地址空间的页表将用于解释所有用户模式内存地址。 这使您能够读取和写入此内存。

[** (设置进程上下文) **](-process--set-process-context-.md)命令的进程具有类似的效果。 但是，**上下文**命令将用户模式地址上下文设置为特定的页面目录，而**process**命令将*进程上下文*设置为特定的进程。 在 x86 处理器上，这两个命令实质上是相同的。 有关更多详细信息，请参阅[处理上下文](changing-contexts.md#process-context)。

如果要进行实时调试，则除了**上下文**命令外，还应发出[**forcedecodeuser**](-cache--set-cache-size-.md)命令。 这会强制调试器查找所需内存空间的物理地址。  (这可能会很慢，因为这通常意味着必须在调试电缆之间传输大量的数据。 ) 

如果正在进行故障转储调试，则不需要[**缓存**](-cache--set-cache-size-.md)命令。 但是，在发生崩溃时，你将无法访问已分页到磁盘的用户模式进程的虚拟地址空间的任何部分。

下面是一个示例。 使用[**！进程**](-process.md)扩展查找所需进程的目录基：

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

现在，请在此页目录基础上使用**上下文**命令。

```dbgcmd
kd> .context 0011f000
```

这使您可以通过多种方式检查地址空间。 例如，以下是[**！ peb**](-peb.md)扩展的输出：

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

 

 





