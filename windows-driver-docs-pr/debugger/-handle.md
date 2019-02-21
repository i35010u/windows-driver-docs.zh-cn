---
title: 句柄
description: 句柄扩展显示有关一个句柄的信息或处理的一个或目标系统中的所有进程都拥有。
ms.assetid: ae3b7e7e-cdc1-4b83-88d7-63fe207044e3
keywords:
- 句柄
- 句柄，句柄扩展
- 处理 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- handle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e4d4c011d120c66d8cd9ade7d019832bf63cca6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521985"
---
# <a name="handle"></a>！ 处理


**！ 处理**或扩展显示有关一个句柄的信息或处理，其中一个在目标系统中的所有进程都拥有。

User-Mode

```dbgcmd
!handle [Handle [UMFlags [TypeName]]] 
!handle -?
```

Kernel-Mode

```dbgcmd
    !handle [Handle [KMFlags [Process [TypeName]]]] 
```

## <a name="span-idddkhandledbgspanspan-idddkhandledbgspanparameters"></a><span id="ddk__handle_dbg"></span><span id="DDK__HANDLE_DBG"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
指定要显示的句柄的索引。 如果*处理*为-1，或如果省略此参数，则调试器会显示与当前进程关联的所有句柄的数据。 如果*处理*为 0，则调试器将显示数据的所有句柄。

<span id="_______UMFlags______"></span><span id="_______umflags______"></span><span id="_______UMFLAGS______"></span> *UMFlags*   
（仅限用户模式）指定显示应包含的内容。 此参数可以是任何以下位值的总和。 （默认值为 0x1。）

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示处理类型信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示基本的句柄的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示处理名称信息。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示特定于对象的句柄的信息，可用时。

<span id="_______KMFlags______"></span><span id="_______kmflags______"></span><span id="_______KMFLAGS______"></span> *KMFlags*   
（仅适用于内核模式）指定显示应包含的内容。 此参数可以是任何以下位值的总和。 （默认值是 0x3。）

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示基本的句柄的信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示有关对象的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示免费处理条目。 如果未设置此位，并省略*处理*或一组它为零，将显示的句柄的列表不包括免费的句柄。 如果*处理*指定的一个免费的句柄，即使不设置此位，它会显示。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
显示来自内核句柄表而不是当前进程的句柄。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
将句柄解释为线程 ID 或进程 ID，并显示相应的内核对象有关的信息。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
（仅适用于内核模式）指定进程。 可以使用的进程 ID 或进程对象的十六进制地址。 此参数必须引用在目标系统上当前正在运行的进程。 如果此参数为-1 或者省略此参数，则使用当前进程。 如果此参数为 0，则显示与所有进程的句柄信息。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span> *TypeName*   
指定你想要检查的句柄的类型。 显示与此类型匹配的手柄。 *TypeName*区分大小写。 有效类型包括事件、 部分、 文件、 端口、 目录、 SymbolicLink、 变化、 windowstation 时，信号量、 密钥、 令牌、 进程、 线程、 桌面、 IoCompletion、 计时器、 作业和 WaitablePort。

<span id="_______-_______"></span> **-?**   
（仅限用户模式）显示此扩展中的一些帮助文本[调试器命令窗口](debugger-command-window.md)。

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
Kdextx86.dll Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p></p>
Kdexts.dll Uext.dll Ntsdexts.dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关控点的详细信息，请参阅[ **！ htrace** ](-htrace.md)扩展、 Microsoft Windows SDK 文档和*Microsoft Windows Internals*作者： Mark Russinovich 和David Solomon。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

可以使用 **！ 处理**用户模式和内核模式下实时调试期间的扩展。 此外可以在内核模式转储文件上使用此扩展。 但是，不能在用户模式转储文件上使用此扩展，除非专门创建了它们与句柄的信息。 (你可以通过创建此类转储文件[ **.dump /mh （创建转储文件）** ](-dump--create-dump-file-.md)命令。)

实时用户模式下在调试期间，可以使用[ **（关闭处理） 的.closehandle** ](-closehandle--close-handle-.md)命令来关闭一个或多个句柄。

下面的示例都是用户模式下 **！ 处理**扩展。 以下命令显示所有句柄的列表。

```dbgcmd
0:000> !handle
Handle 4
  Type          Section
Handle 8
  Type          Event
Handle c
  Type          Event
Handle 10
  Type          Event
Handle 14
  Type          Directory
Handle 5c
  Type          File
6 Handles
Type            Count
Event           3
Section         1
File            1
Directory       1
```

下面的命令显示有关句柄 0x8 的详细的信息。

```dbgcmd
0:000> !handle 8 f
Handle 8
  Type          Event
  Attributes    0
  GrantedAccess 0x100003:
         Synch
         QueryState,ModifyState
  HandleCount   2
  PointerCount  3
  Name          <none>
  Object Specific Information
    Event Type Auto Reset
    Event is Waiting
```

下面的示例是内核模式的示例 **！ 处理**。 以下命令将列出所有句柄，包括免费的句柄。

```dbgcmd
kd> !handle 0 4
processor number 0
PROCESS 80559800  SessionId: 0  Cid: 0000    Peb: 00000000  ParentCid: 0000
    DirBase: 00039000  ObjectTable: e1000d60  TableSize: 380.
    Image: Idle

New version of handle table at e1002000 with 380 Entries in use

0000: free handle, Entry address e1002000, Next Entry fffffffe
0004: Object: 80ed5238  GrantedAccess: 001f0fff
0008: Object: 80ed46b8  GrantedAccess: 00000000
000c: Object: e1281d00  GrantedAccess: 000f003f
0010: Object: e1013658  GrantedAccess: 00000000
......
0168: Object: ffb6c748  GrantedAccess: 00000003 (Protected)
016c: Object: ff811f90  GrantedAccess: 0012008b
0170: free handle, Entry address e10022e0, Next Entry 00000458
0174: Object: 80dfd5c8  GrantedAccess: 001f01ff
......
```

以下命令显示内核句柄表中的句柄 0x14 有关的详细的信息。

```dbgcmd
kd> !handle 14 13
processor number 0
PROCESS 80559800  SessionId: 0  Cid: 0000    Peb: 00000000  ParentCid: 0000
    DirBase: 00039000  ObjectTable: e1000d60  TableSize: 380.
    Image: Idle

Kernel New version of handle table at e1002000 with 380 Entries in use
0014: Object: e12751d0  GrantedAccess: 0002001f
Object: e12751d0  Type: (80ec8db8) Key
    ObjectHeader: e12751b8
        HandleCount: 1  PointerCount: 1
        Directory Object: 00000000  Name: \REGISTRY\MACHINE\SYSTEM\CONTROLSET001\CONTROL\SESSION MANAGER\EXECUTIVE
```

以下命令显示所有进程中所有对象的句柄部分有关的信息。

```dbgcmd
!handle 0 3 0 Section
...
PROCESS fffffa8004f48940
    SessionId: none  Cid: 0138    Peb: 7f6639bf000  ParentCid: 0004
    DirBase: 10cb74000  ObjectTable: fffff8a00066f700  HandleCount:  39.
    Image: smss.exe

Handle table at fffff8a00066f700 with 39 entries in use

0040: Object: fffff8a000633f00  GrantedAccess: 00000006 (Inherit) Entry: fffff8a000670100
Object: fffff8a000633f00  Type: (fffffa80035fef20) Section
    ObjectHeader: fffff8a000633ed0 (new version)
        HandleCount: 1  PointerCount: 262144
...
```

 

 





