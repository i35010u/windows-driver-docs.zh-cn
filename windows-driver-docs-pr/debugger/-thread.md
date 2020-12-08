---
title: 线程 (thread)
description: 线程扩展显示有关目标系统上的线程的摘要信息，包括 ETHREAD 块。 此命令只能在内核模式调试过程中使用。
keywords:
- 线程 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b8a6543fb8a625901e8816f010c9673e9dbfe43e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830311"
---
# <a name="thread"></a>!thread


**！线程** 扩展显示有关目标系统上的线程的摘要信息，包括 ETHREAD 块。 此命令只能在内核模式调试过程中使用。

此扩展命令不同于 [**. 线程 (设置注册上下文)**](-thread--set-register-context-.md) 命令。

语法

```dbgcmd
!thread [-p] [-t] [Address [Flags]]
```

## <a name="span-idddk__thread_dbgspanspan-idddk__thread_dbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>参数


<span id="_______-p______"></span><span id="_______-P______"></span>**-p**   
显示有关拥有线程的进程的摘要信息。

<span id="_______-t______"></span><span id="_______-T______"></span>**-t**   
如果包括此选项，则 *Address* 为线程 ID，而不是线程地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定目标计算机上的线程的十六进制地址。 如果 *Address* 为-1 或省略，则指示当前线程。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的详细信息的级别。 *标志* 可以是以下位的任意组合。 如果 *Flags* 为0，则只显示最少数量的信息。 默认值为0x6：

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示线程的等待状态。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
如果在没有位 1 (0x2) 的情况下使用此位，则不起作用。 如果此位与位1一起使用，则该线程将显示堆栈跟踪。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
将) **bsp** 寄存器值的 Itanium 系统上的返回地址、堆栈指针和 (添加到为每个函数显示的信息，并禁止显示函数参数。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
将进程上下文设置为等于此命令持续时间内拥有指定线程的进程。 这将导致更准确地显示线程堆栈。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内核模式下的线程的信息，请参阅 [更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。

<a name="remarks"></a>备注
-------

下面是一个使用 Windows 10 的示例：

```dbgcmd
0: kd> !thread 0xffffcb088f0a4480            
THREAD ffffcb088f0a4480  Cid 0e34.3814  Teb: 0000001a27ca6000 Win32Thread: 0000000000000000 RUNNING on processor 0
Not impersonating
DeviceMap                 ffffb80842016c20
Owning Process            ffffcb08905397c0       Image:         MsMpEng.exe
Attached Process          N/A            Image:         N/A
Wait Start TickCount      182835891      Ticks: 0
Context Switch Count      5989           IdealProcessor: 3             
UserTime                  00:00:01.046
KernelTime                00:00:00.296
Win32 Start Address 0x00007ffb3b2fd1b0
Stack Init ffff95818476add0 Current ffff958184769d30
Base ffff95818476b000 Limit ffff958184765000 Call 0000000000000000
Priority 8 BasePriority 8 PriorityDecrement 0 IoPriority 2 PagePriority 5
Child-SP          RetAddr           : Args to Child                                                           : Call Site
fffff802`59858c68 fffff801`b56d24aa : ffffcb08`8fd68010 00000000`00000000 fffff802`58259600 00000000`00000008 : nt!DbgBreakPointWithStatus [d:\rs2\minkernel\ntos\rtl\amd64\debugstb.asm @ 130] 
fffff802`59858c70 ffffcb08`8fd68010 : 00000000`00000000 fffff802`58259600 00000000`00000008 ffffcb08`8f0a4400 : 0xfffff801`b56d24aa
fffff802`59858c78 00000000`00000000 : fffff802`58259600 00000000`00000008 ffffcb08`8f0a4400 00000000`00000019 : 0xffffcb08`8fd68010
```

使用类似于 [**！进程**](-process.md) 的命令查找你感兴趣的线程的地址或线程 ID。

下表说明了 **！线程** 显示中有用的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>线程地址</strong></p></td>
<td align="left"><p>字词 <em>线程</em> 后的十六进制数是 ETHREAD 块的地址。 在前面的示例中，线程地址为0xffffcb088f0a4480。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>线程 ID</strong></p></td>
<td align="left"><p>Word <em>Cid</em> 后面的两个十六进制数字是进程 id 和线程 id：进程 id <em>。线程 id</em>。 在前面的示例中，进程 ID 为0x0e34，线程 ID 为0x3814。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>线程环境块 (TEB) </strong></p></td>
<td align="left"><p>单词 <em>Teb</em> 后面的十六进制数字是线程环境块 (Teb) 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>系统服务调度表</strong></p></td>
<td align="left"><p>单词 <em>Win32Thread</em> 后面的十六进制数是系统服务调度表的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>线程状态</strong></p></td>
<td align="left"><p>线程状态显示在以 <em>运行</em>单词开头的行的末尾。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>拥有进程</strong></p></td>
<td align="left"><p>拥有此线程的进程的 EPROCESS 地址是其 <em>所属</em> 进程的十六进制数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>起始地址</strong></p></td>
<td align="left"><p>字词 <em>开始地址</em> 后面的十六进制数是线程起始地址。 这可能会以符号形式出现。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>用户线程函数</strong></p></td>
<td align="left"><p>词 <em>Win32 起始地址</em> 后的十六进制数是用户线程函数的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Priority</strong></p></td>
<td align="left"><p>线程的优先级信息遵循 word <em>优先级</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>堆栈跟踪</strong></p></td>
<td align="left"><p>此显示的结束时，将显示线程的堆栈跟踪。</p></td>
</tr>
</tbody>
</table>

 

 

 





