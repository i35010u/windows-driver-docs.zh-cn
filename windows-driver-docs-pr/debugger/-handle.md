---
title: 句柄
description: 句柄扩展显示有关句柄的信息, 或处理目标系统中的一个或所有进程。
ms.assetid: ae3b7e7e-cdc1-4b83-88d7-63fe207044e3
keywords:
- 句柄
- 句柄, 句柄扩展
- 处理 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- handle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0f1b81b8f88633f7d64fe6e245f1917fa0ceb71
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025241"
---
# <a name="handle"></a>!handle


**! Handle** extension 显示有关句柄的信息, 或处理目标系统中的一个或所有进程。

用户模式

```dbgcmd
!handle [Handle [UMFlags [TypeName]]] 
!handle -?
```

内核模式

```dbgcmd
    !handle [Handle [KMFlags [Process [TypeName]]]] 
```

## <a name="span-idddk__handle_dbgspanspan-idddk__handle_dbgspanparameters"></a><span id="ddk__handle_dbg"></span><span id="DDK__HANDLE_DBG"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
指定要显示的句柄的索引。 如果*Handle*为-1 或省略此参数, 调试器将显示与当前进程关联的所有句柄的数据。 如果*Handle*为 0, 则调试器将显示所有句柄的数据。

<span id="_______UMFlags______"></span><span id="_______umflags______"></span><span id="_______UMFLAGS______"></span>*UMFlags*   
(仅用户模式)指定显示内容应包含的内容。 此参数可以是以下任何位值的总和。 (默认值为0x1。)

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示句柄类型信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示基本句柄信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示句柄名称信息。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示特定于对象的句柄信息 (如果可用)。

<span id="_______KMFlags______"></span><span id="_______kmflags______"></span><span id="_______KMFLAGS______"></span>*KMFlags*   
(仅限内核模式)指定显示内容应包含的内容。 此参数可以是以下任何位值的总和。 (默认值为0x3。)

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示基本句柄信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示有关对象的信息。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示可用的句柄项。 如果未设置此位并且省略了*句柄*或将其设置为零, 则显示的句柄列表不包含可用的句柄。 如果*handle*指定单个自由句柄, 则即使未设置此位, 也会显示该句柄。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)  
显示来自内核句柄表而不是当前进程的句柄。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>位 5 (0x20)  
将句柄解释为线程 ID 或进程 ID, 并显示有关相应内核对象的信息。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
(仅限内核模式)指定进程。 您可以使用进程 ID 或进程对象的十六进制地址。 此参数必须引用目标系统上当前正在运行的进程。 如果此参数为-1 或省略此参数, 则使用当前进程。 如果此参数为 0, 则显示所有进程中的 "处理信息"。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span>*TypeName*   
指定要检查的句柄的类型。 只显示匹配此类型的句柄。 *TypeName*区分大小写。 有效类型包括事件、节、文件、端口、目录、SymbolicLink、变化、Windowstation 时出错、信号量、密钥、令牌、进程、线程、桌面、IoCompletion、计时器、作业和 WaitablePort。

<span id="_______-_______"></span> **-?**    
(仅用户模式)在[调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

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
Kdextx86 Ntsdexts Uext. .dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p></p>
Kdexts Ntsdexts Uext. .dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关句柄的详细信息, 请参阅[ **! htrace**](-htrace.md) extension、Microsoft Windows SDK 文档和*Microsoft Windows 内部机制*, Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

你可以在用户模式和内核模式实时调试过程中使用 **! 句柄**扩展。 你还可以在内核模式转储文件中使用此扩展。 但是, 你不能对用户模式转储文件使用此扩展, 除非你专门使用处理信息创建它们。 (可以使用[**dump/mh (创建转储文件)** ](-dump--create-dump-file-.md)命令创建此类转储文件。)

在实时用户模式调试过程中, 可以使用[**closehandle (关闭句柄)** ](-closehandle--close-handle-.md)命令关闭一个或多个句柄。

以下示例是 **! 句柄**扩展的用户模式示例。 以下命令显示所有句柄的列表。

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

以下命令显示有关句柄0x8 的详细信息。

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

以下示例是 **! handle**的内核模式示例。 以下命令将列出所有句柄, 包括自由句柄。

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

以下命令显示有关内核句柄表中的句柄0x14 的详细信息。

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

以下命令显示有关所有进程中的 Section 对象的所有句柄的信息。

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

 

 





