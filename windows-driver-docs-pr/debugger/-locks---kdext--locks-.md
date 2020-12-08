---
title: 锁定 kdext
description: Kdextx86.dll 和 Kdexts.dll 中的锁扩展显示有关内核 ERESOURCE 锁的信息。
keywords:
- kdext 锁扩展
- ERESOURCE 锁
- 死锁
- 锁定 kdext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( kdext .locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 048b0258c1f1813742bf595efb6ac7d3de7c66ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803321"
---
# <a name="locks-kdextlocks"></a>！锁 (！ kdext \*) 


Kdextx86.dll 和 Kdexts.dll 中的 **！锁** 扩展显示有关内核 ERESOURCE 锁的信息。

此扩展命令不应与 [**！ ntsdexts**](-locks---ntsdexts-locks-.md) extension 命令混淆。

```dbgcmd
!locks [Options] [Address]
```

## <a name="span-idddk__kdext__locks_dbgspanspan-idddk__kdext__locks_dbgspanparameters"></a><span id="ddk__kdext__locks_dbg"></span><span id="DDK__KDEXT__LOCKS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定要显示的信息量。 可以使用下列选项的任意组合：

<span id="-v"></span><span id="-V"></span>**-v**  
显示有关每个锁定的详细信息。

<span id="-p"></span><span id="-P"></span>**-p**  
显示有关锁的所有可用信息，包括性能统计信息。

<span id="-d"></span><span id="-D"></span>**-d.ddd...e**  
显示有关所有锁的信息。 否则，只显示具有争用的锁。 ) 

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的 ERESOURCE 锁的十六进制地址。 如果 *Address* 为0或省略，将显示系统中所有 ERESOURCE 锁的相关信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**！锁** 扩展显示按线程保存在资源上的所有锁。 锁定可以是共享的，也可以是独占的，这意味着没有其他线程可以获取对该资源的访问权限。 当系统上发生死锁时，此信息很有用。 死锁是指在执行线程所需的资源上持有排他锁的非执行线程。

通常可以通过查找一个在执行线程所需的资源上持有排他锁的非执行线程，来找出 Microsoft Windows 2000 中的死锁。 大多数锁都是共享的。

下面是基本 **！锁** 输出的示例：

```dbgcmd
kd> !locks
**** DUMP OF ALL RESOURCE OBJECTS ****
KD: Scanning for held locks......

Resource @ 0x80e97620    Shared 4 owning threads
     Threads: ff688da0-01<*> ff687da0-01<*> ff686da0-01<*> ff685da0-01<*> 
KD: Scanning for held locks.......................................................

Resource @ 0x80e23f38    Shared 1 owning threads
     Threads: 80ed0023-01<*> *** Actual Thread 80ed0020
KD: Scanning for held locks.

Resource @ 0x80d8b0b0    Shared 1 owning threads
     Threads: 80ed0023-01<*> *** Actual Thread 80ed0020
2263 total locks, 3 locks currently held
```

请注意，显示的每个线程的地址后跟其线程计数 (例如，"-01" ) 。 如果某个线程后跟 " &lt; \* &gt; "，则该线程是该锁的所有者之一。 在某些情况下，初始线程地址包含偏移量。 在这种情况下，也会显示实际的线程地址。

如果要查找有关这些资源对象之一的详细信息，请使用后面的 "资源 \@ " 地址作为自变量，以供将来的命令使用。 若要调查上一个示例中显示的第二个资源，可以使用 [**DT ERESOURCE 80d8b0b0**](dt--display-type-.md) 或 [**！ thread 80ed0020**](-thread.md)。 或者，可以使用 **-v** 选项再次使用 **！锁** 扩展：

```dbgcmd
kd> !locks -v 80d8b0b0

Resource @ 0x80d8b0b0    Shared 1 owning threads
     Threads: 80ed0023-01<*> *** Actual Thread 80ed0020

     THREAD 80ed0020  Cid 4.2c  Teb: 00000000 Win32Thread: 00000000 WAIT: (WrQueue) KernelMode Non-Alertable
         8055e100  Unknown
     Not impersonating
GetUlongFromAddress: unable to read from 00000000
     Owning Process 80ed5238
     WaitTime (ticks)          44294977
     Context Switch Count      147830             
     UserTime                  0:00:00.0000
     KernelTime                0:00:02.0143
     Start Address nt!ExpWorkerThread (0x80506aa2)
     Stack Init fafa4000 Current fafa3d18 Base fafa4000 Limit fafa1000 Call 0
     Priority 13 BasePriority 13 PriorityDecrement 0
ChildEBP RetAddr  
fafa3d30 804fe997 nt!KiSwapContext+0x25 (FPO: [EBP 0xfafa3d48] [0,0,4]) [D:\NT\base\ntos\ke\i386\ctxswap.asm @ 139]
fafa3d48 80506a17 nt!KiSwapThread+0x85 (FPO: [Non-Fpo]) (CONV: fastcall) [d:\nt\base\ntos\ke\thredsup.c @ 1960]
fafa3d78 80506b36 nt!KeRemoveQueue+0x24c (FPO: [Non-Fpo]) (CONV: stdcall) [d:\nt\base\ntos\ke\queueobj.c @ 542]
fafa3dac 805ad8bb nt!ExpWorkerThread+0xc6 (FPO: [Non-Fpo]) (CONV: stdcall) [d:\nt\base\ntos\ex\worker.c @ 1130]
fafa3ddc 8050ec72 nt!PspSystemThreadStartup+0x2e (FPO: [Non-Fpo]) (CONV: stdcall) [d:\nt\base\ntos\ps\create.c @ 2164]
00000000 00000000 nt!KiThreadStartup+0x16 [D:\NT\base\ntos\ke\i386\threadbg.asm @ 81]

1 total locks, 1 locks currently held
```

 

 





