---
title: peb
description: Peb 扩展在进程环境块 (PEB) 中显示信息的格式化的的视图。
ms.assetid: 01687f13-9eb7-48f0-a0d6-54fee00084ab
keywords:
- PEB （进程环境块）
- 过程中，进程环境块 (PEB)
- peb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- peb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b8d30605c25ad6839ab818329ef470d1b9d27de
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238522"
---
# <a name="peb"></a>!peb


**！ Peb**扩展在进程环境块 (PEB) 中显示的信息的格式化的视图。

```dbgcmd
!peb [PEB-Address]
```

## <a name="span-idddkpebdbgspanspan-idddkpebdbgspanparameters"></a><span id="ddk__peb_dbg"></span><span id="DDK__PEB_DBG"></span>参数


<span id="_______PEB-Address______"></span><span id="_______peb-address______"></span><span id="_______PEB-ADDRESS______"></span> *PEB-Address*   
过程你想要检查其 PEB 的十六进制的地址。 （这不是如派生自该过程的内核 process 块 PEB 的地址。）如果*PEB 地址*将使用在当前进程在用户模式下，PEB 省略。 如果省略在内核模式下，对应于当前 PEB[进程上下文](changing-contexts.md#process-context)显示。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关进程环境块的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 

<a name="remarks"></a>备注
-------

PEB 是 Microsoft Windows 进程控制结构的用户模式部分。

如果 **！ peb**扩展使用没有自变量为你提供错误在内核模式下，应使用[ **！ 过程**](-process.md)扩展来确定所需的进程的 PEB 地址。 请确保你[进程上下文](changing-contexts.md#process-context)是设置为所需的进程，以及如何为参数将 PEB 地址 **！ peb**。

显示的确切输出取决于 Windows 版本以及调试在内核模式或用户模式。 下面的示例取自内核调试程序附加到 Windows Server 2003 目标：

```dbgcmd
kd> !peb
PEB at 7ffdf000
    InheritedAddressSpace:    No
    ReadImageFileExecOptions: No
    BeingDebugged:            No
    ImageBaseAddress:         4ad00000
    Ldr                       77fbe900
    Ldr.Initialized:          Yes
    Ldr.InInitializationOrderModuleList: 00241ef8 . 00242360
    Ldr.InLoadOrderModuleList:           00241e90 . 00242350
    Ldr.InMemoryOrderModuleList:         00241e98 . 00242358
            Base TimeStamp                     Module
        4ad00000 3d34633c Jul 16 11:17:32 2002 D:\WINDOWS\system32\cmd.exe
        77f40000 3d346214 Jul 16 11:12:36 2002 D:\WINDOWS\system32\ntdll.dll
        77e50000 3d3484ef Jul 16 13:41:19 2002 D:\WINDOWS\system32\kernel32.dll
....
    SubSystemData:     00000000
    ProcessHeap:       00140000
    ProcessParameters: 00020000
    WindowTitle:  'D:\Documents and Settings\Administrator\Desktop\Debuggers.lnk'
    ImageFile:    'D:\WINDOWS\system32\cmd.exe'
    CommandLine:  '"D:\WINDOWS\system32\cmd.exe" '
    DllPath:      'D:\WINDOWS\system32;D:\WINDOWS\system32;....
    Environment:  00010000
        ALLUSERSPROFILE=D:\Documents and Settings\All Users
        APPDATA=D:\Documents and Settings\UserTwo\Application Data
        CLIENTNAME=Console
....
        windir=D:\WINDOWS
```

类似[ **！ teb** ](-teb.md)扩展显示的线程环境块。

 

 





