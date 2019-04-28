---
title: 锁 kdext
description: Kdextx86.dll 和 Kdexts.dll 中的锁扩展显示有关内核 ERESOURCE 锁的信息。
ms.assetid: c1be6c6c-0028-459f-9c92-61df52cbc4b6
keywords:
- kdext 锁扩展
- ERESOURCE 锁
- 死锁
- 锁 kdext.locks Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( kdext .locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6bcef64132d52b5f0d4af99fbb45c4353e5dd25b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336162"
---
# <a name="locks-kdextlocks"></a>！ 锁 (！ kdext\*.locks)


**！ 锁**Kdextx86.dll 和 Kdexts.dll 中的扩展显示有关内核 ERESOURCE 锁的信息。

不要将此扩展命令与相混淆[ **！ ntsdexts.locks** ](-locks---ntsdexts-locks-.md)扩展命令。

```dbgcmd
!locks [Options] [Address]
```

## <a name="span-idddkkdextlocksdbgspanspan-idddkkdextlocksdbgspanparameters"></a><span id="ddk__kdext__locks_dbg"></span><span id="DDK__KDEXT__LOCKS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
指定要显示的信息。 可以使用以下选项的任意组合：

<span id="-v"></span><span id="-V"></span>**-v**  
显示有关每个锁的详细的信息。

<span id="-p"></span><span id="-P"></span>**-p**  
显示有关包括性能统计信息的锁的所有可用信息。

<span id="-d"></span><span id="-D"></span>**-d**  
显示有关所有锁的信息。 否则，仅锁争用将显示。）

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的 ERESOURCE 锁定十六进制的地址。 如果*地址*为 0 或省略，就会显示在系统中的所有 ERESOURCE 锁有关的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

**！ 锁**扩展插件都会显示所有线程上的资源持有的锁。 可以共享锁或排他，这意味着没有其他线程可以访问该资源。 在系统上发生死锁时，此信息很有用。 死锁引起非正在执行的一个线程上执行的线程需要的资源持有排他锁。

你通常可以通过查找对资源所需的执行线程持有排他锁的一个非执行线程准确定位在 Microsoft Windows 2000 死锁。 共享锁的大多数。

下面是基本的示例 **！ 锁**输出：

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

请注意，每个线程的地址显示后跟其线程计数 (例如，"-01")。 如果一个线程后跟"&lt;\*&gt;"，线程是某个锁的所有者。 在某些情况下，初始线程地址包含某一偏移量。 在这种情况下，还显示的实际线程地址。

如果你想要找到其中某个资源对象的详细信息，使用下面的地址"资源 @"为后续命令的参数。 若要调查中前面的示例中所示的第二个资源，可以使用[ **dt ERESOURCE 80d8b0b0** ](dt--display-type-.md)或[ **！ 线程 80ed0020** ](-thread.md). 或者，可以使用 **！ 锁**再次扩展 **-v**选项：

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

 

 





