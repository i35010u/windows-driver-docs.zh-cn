---
title: peb
description: Peb 扩展在进程环境块 (PEB) 中显示信息的格式化视图。
keywords:
- 'PEB (进程环境块) '
- '进程环境块 (PEB) '
- peb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- peb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb6fd45213d327afc3eff8fa2572d9adc5061ab3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805807"
---
# <a name="peb"></a>!peb


**！ Peb** 扩展显示 (peb) 的进程环境块中的信息的格式化视图。

```dbgcmd
!peb [PEB-Address]
```

## <a name="span-idddk__peb_dbgspanspan-idddk__peb_dbgspanparameters"></a><span id="ddk__peb_dbg"></span><span id="DDK__PEB_DBG"></span>参数


<span id="_______PEB-Address______"></span><span id="_______peb-address______"></span><span id="_______PEB-ADDRESS______"></span>*PEB-地址*   
要检查其 PEB 的进程的十六进制地址。  (这不是从进程的内核进程块派生的 PEB 的地址。 ) 如果在用户模式下省略 *PEB* ，则使用当前进程的 PEB。 如果在内核模式下省略此方法，则将显示与当前 [进程上下文](changing-contexts.md#process-context) 相对应的 PEB。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关进程环境块的信息，请参阅 *Microsoft Windows 内部机制* ，标记 Russinovich 和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

PEB 是 Microsoft Windows 进程控制结构的用户模式部分。

如果没有参数的 **！ peb** 扩展在内核模式下出现错误，则应使用 [**！进程**](-process.md) 扩展来确定所需进程的 peb 地址。 请确保将你的 [进程上下文](changing-contexts.md#process-context) 设置为所需的进程，然后使用 PEB 地址作为 **！ PEB** 的参数。

显示的确切输出取决于 Windows 版本以及是在内核模式下还是在用户模式下进行调试。 以下示例取自附加到 Windows Server 2003 目标的内核调试器：

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

类似的 [**！ teb**](-teb.md) 扩展显示线程环境块。

 

 





