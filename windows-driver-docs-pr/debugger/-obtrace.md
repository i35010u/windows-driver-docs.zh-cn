---
title: obtrace
description: Obtrace 扩展显示指定的对象的对象引用跟踪数据。
ms.assetid: 6a124f9f-1c2f-4303-b84f-0032fb912cc1
keywords:
- obtrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- obtrace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28eb455d377c3ce9e0442528aa2291f9240b1d0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334472"
---
# <a name="obtrace"></a>!obtrace


**！ Obtrace**扩展显示指定的对象的对象引用跟踪数据。

```dbgcmd
!obtrace Object
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
一个指向该对象或路径。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关全局标志实用工具 (GFlags) 的详细信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

只要对象引用计数器递增或递减，Windows 的对象引用跟踪功能记录顺序的堆栈跟踪。

然后再使用此扩展显示的对象引用跟踪数据，必须使用[GFlags](gflags.md)以启用[对象引用跟踪](object-reference-tracing.md)指定的对象。 可以启用作为内核标志 （运行） 设置，在其中更改将立即生效，但消失后关闭或重新启动; 如果对象引用跟踪或者，作为注册表设置，这需要重启，但在更改之前保持有效。

下面是输出的示例 **！ obtrace**扩展：

```dbgcmd
kd> !obtrace 0xfa96f700
Object: fa96f700        Image: cmd.exe
Sequence  (+/-)  Stack
--------  -----  ---------------------------------------------------
   2421d    +1  nt!ObCreateObject+180
                nt!NtCreateEvent+92
                nt!KiFastCallEntry+104
                nt!ZwCreateEvent+11
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   2421e    -1  nt!ObfDereferenceObject+19
                nt!NtCreateEvent+d4
                nt!KiFastCallEntry+104
                nt!ZwCreateEvent+11
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   2421f    +1  nt!ObReferenceObjectByHandle+1c3
                win32k!xxxCreateThreadInfo+37d
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   24220    +1  nt!ObReferenceObjectByHandle+1c3
                win32k!ProtectHandle+22
                win32k!xxxCreateThreadInfo+3a0
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

   24221    -1  nt!ObfDereferenceObject+19
                win32k!xxxCreateThreadInfo+3a0
                win32k!UserThreadCallout+6f
                win32k!W32pThreadCallout+38
                nt!PsConvertToGuiThread+174
                nt!KiBBTUnexpectedRange+c

----  ----------------------------------------------------------
References: 3, Dereferences 2
```

中的主要指标 **！ obtrace 0xfa96f700**显示下表中列出。

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
<td align="left"><p><strong>序列</strong></p></td>
<td align="left"><p>表示操作的顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>+/-</strong></p></td>
<td align="left"><p>指示引用或取消引用操作。</p>
<p>+ 1 指示引用操作。</p>
<p>-1 指示取消引用操作。</p>
<p>+ /-n 指示多个引用/取消引用操作。</p></td>
</tr>
</tbody>
</table>

 

基于 x64 的目标计算机上的对象引用跟踪可能会不完整，因为它不是始终可以获取堆栈跟踪在 IRQL 级别高于被动\_级别。

可以通过按 CTRL + BREAK （在 WinDbg) 或 （在 KD) CTRL + C 来停止在任何时间执行。

 

 





