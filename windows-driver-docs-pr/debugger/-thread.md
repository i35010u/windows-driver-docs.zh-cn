---
title: 线程
description: 线程扩展目标系统，其中包括 ETHREAD 块上显示一个线程的摘要信息。 可以在内核模式调试期间仅使用此命令。
ms.assetid: 5d3cf2f7-02bf-4a94-b542-826ad2b66a6f
keywords:
- Windows 调试的线程
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c9c5218b648e32736a70323cca9d32920b1d51a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567327"
---
# <a name="thread"></a>!thread


**！ 线程**扩展目标系统，其中包括 ETHREAD 块上显示一个线程的摘要信息。 可以在内核模式调试期间仅使用此命令。

此扩展命令不是与相同[ **.thread （设置注册上下文）** ](-thread--set-register-context-.md)命令。

语法

```dbgcmd
!thread [-p] [-t] [Address [Flags]]
```

## <a name="span-idddkthreaddbgspanspan-idddkthreaddbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>参数


<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
显示拥有该线程的进程的摘要信息。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
包括此选项，则当*地址*是线程 ID，而不是线程的地址。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
在目标计算机上指定的线程的十六进制地址。 如果*地址*为-1 或省略，指示当前线程。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要显示详细信息的级别。 *标志*可以是以下位的任意组合。 如果*标志*为 0，则显示只有少量的信息。 默认值为 0x6:

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示线程的等待状态。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
如果不包含位 1 (0x2) 使用此位，则它不起。 如果此位用于位 1，线程被显示堆栈跟踪。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
将返回地址，堆栈指针中，添加和 （Itanium 系统） 上**bsp**注册值显示为每个函数的信息，并禁止显示函数自变量。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
将进程上下文设置为等于此命令的持续时间内拥有指定的线程的进程。 这会导致线程堆栈的更准确地显示。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关内核模式中的线程的信息，请参阅[更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

下面是使用 Windows 10 的示例：

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

使用命令，例如[ **！ 过程**](-process.md)定位地址或线程感兴趣的线程 ID。

中的有用信息 **！ 线程**显示下表中所述。

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
<td align="left"><p>单词后面的十六进制数字<em>线程</em>是 ETHREAD 块的地址。 在上述示例中，线程地址为 0xffffcb088f0a4480。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>线程 ID</strong></p></td>
<td align="left"><p>在该词后面的两个十六进制数字<em>Cid</em>进程 ID 和线程 ID:<em>进程 ID.thread ID</em>。 在前面的示例中，进程 ID 是 0x0e34，和线程 ID 是 0x3814。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>线程环境块 (TEB)</strong></p></td>
<td align="left"><p>单词后面的十六进制数字<em>Teb</em>是线程环境块 (TEB) 的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>系统服务调度表</strong></p></td>
<td align="left"><p>单词后面的十六进制数字<em>Win32Thread</em>是系统服务调度表的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>线程状态</strong></p></td>
<td align="left"><p>线程状态显示在开头的词的行的末尾<em>运行</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>拥有进程</strong></p></td>
<td align="left"><p>单词后面的十六进制数字<em>拥有进程</em>是拥有此线程的进程 EPROCESS 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>起始地址</strong></p></td>
<td align="left"><p>单词后面的十六进制数字<em>起始地址</em>线程开始地址。 这可能以符号的形式显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>用户线程函数</strong></p></td>
<td align="left"><p>单词后面的十六进制数字<em>Win32 起始地址</em>是用户线程函数的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>优先级</strong></p></td>
<td align="left"><p>线程的优先级信息遵循单词<em>优先级</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>堆栈跟踪</strong></p></td>
<td align="left"><p>在此显示的最后阶段显示线程的堆栈跟踪。</p></td>
</tr>
</tbody>
</table>

 

 

 





