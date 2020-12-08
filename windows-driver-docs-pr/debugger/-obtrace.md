---
title: obtrace
description: Obtrace 扩展显示指定对象的对象引用跟踪数据。
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
ms.openlocfilehash: c20f7ca26f35dd0bbc8d28a3e079eed3615e0c5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795225"
---
# <a name="obtrace"></a>!obtrace


**！ Obtrace** extension 显示指定对象的对象引用跟踪数据。

```dbgcmd
!obtrace Object
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
指向对象或路径的指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关全球标志实用程序 (GFlags) 的详细信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

每当对象引用计数器递增或递减时，Windows 的对象引用跟踪功能都将记录顺序堆栈跟踪。

使用此扩展显示对象引用跟踪数据之前，必须使用 [GFlags](gflags.md) 为指定的对象启用 [对象引用跟踪](object-reference-tracing.md) 。 您可以启用对象引用跟踪作为内核标志 (运行时) 设置，更改将立即生效，但如果关闭或重新启动，则会消失;或者作为注册表设置，这需要重新启动，但在更改之前仍有效。

下面是 **！ obtrace** 扩展的输出示例：

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

下表列出了 **！ obtrace 0xfa96f700** 显示的主要指标。

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
<td align="left"><p>表示运算的顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>+/-</strong></p></td>
<td align="left"><p>指示引用或取消引用操作。</p>
<p>+ 1 表示引用操作。</p>
<p>-1 表示取消引用操作。</p>
<p>+/-n 指示多次引用/取消引用操作。</p></td>
</tr>
</tbody>
</table>

 

基于 x64 的目标计算机上的对象引用跟踪可能是不完整的，因为并非总是可以在比被动级别更高的 IRQL 级别获取堆栈跟踪 \_ 。

您可以随时通过按) 中的 CTRL + BREAK (，或在 KD) 中按 CTRL + C (停止执行。

 

 





