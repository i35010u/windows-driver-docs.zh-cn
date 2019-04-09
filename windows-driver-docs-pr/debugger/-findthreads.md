---
title: findthreads
description: Findthreads 扩展提供的搜索条件的目标系统上显示有关一个或多个线程的摘要信息。
ms.assetid: ED14E503-0AF2-4444-81B0-7E00A6E424E5
keywords:
- findthreads Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- findthreads
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d8de83a1055a9af0c0e6a8cc0efc810951365fc
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239478"
---
# <a name="findthreads"></a>!findthreads


！ Findthreads 扩展提供的搜索条件的目标系统上显示有关一个或多个线程的摘要信息。 当关联的堆栈引用所提供的对象时，将显示线程信息。 可以在内核模式调试期间仅使用此命令。

语法

```dbgcmd
!findthreads [-v][-t  <Thread Address>|-i <IRP Address>|-d <Device Address>|( -a <Pointer Address> -e <End Address> | -l <Range Length>)] 
```

## <a name="span-idddkthreaddbgspanspan-idddkthreaddbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示条件的所有匹配项的详细信息。

<span id="_______-t_Thread_Address______"></span><span id="_______-t_thread_address______"></span><span id="_______-T_THREAD_ADDRESS______"></span> **-t** **** *线程地址*   
搜索条件将所有模块、 等待对象和 Irp 的线程，以及设备对象和附加 Irp 从生成的模块。 此选项通常将提供最广泛的搜索条件。

<span id="_______-i_IRP_Address____________"></span><span id="_______-i_irp_address____________"></span><span id="_______-I_IRP_ADDRESS____________"></span> **-i** **** *IRP Address*   
搜索条件将所有模块和所指示的 IRP，以及对 IRP 本身的任何引用的设备。

<span id="_______-d_Device_Address____________"></span><span id="_______-d_device_address____________"></span><span id="_______-D_DEVICE_ADDRESS____________"></span> **-d** **** *设备地址*   
将设备对象从基于搜索条件。 这将包括该模块 （通过驱动程序对象） 的设备对象与关联设备扩展，任何 IRP 附加到设备，以及任何附加到的设备对象的类似信息。

<span id="_______-a_Pointer_Address____________"></span><span id="_______-a_pointer_address____________"></span><span id="_______-A_POINTER_ADDRESS____________"></span> **-a** **** *指针地址*   
将基址添加到条件。 如果正确指定-e 或-l，此值将为内存范围的基础。 否则，它被解释为一个指针。

<span id="_______-e_End_Address____________"></span><span id="_______-e_end_address____________"></span><span id="_______-E_END_ADDRESS____________"></span> **-e** **** *结束地址*   
指定的与指定的内存范围的结束地址。

<span id="_______-l_Range_Length______"></span><span id="_______-l_range_length______"></span><span id="_______-L_RANGE_LENGTH______"></span> **-l** **** *范围长度*   
指定-使用指定的内存范围的长度。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 10 和更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关内核模式中的线程的信息，请参阅[更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

下面是示例输出使用-v，-t 选项：

```dbgcmd
kd> !findthreads -v -t ffffd001ee29cdc0

Added criterion for THREAD 0xffffd001ee29cdc0
  Added criterion for THREAD STACK 0xffffd001ee2bac20
  ERROR: Object 0xffffffffffffffe0 is not an IRP
ERROR: unable to completely walk thread IRP list.
  Added criterion for MODULE kdnic(0xfffff80013120000)

Found 63 threads matching the search criteria

Found 6 criteria matches for THREAD 0xffffe0016a383740, PROCESS 0xffffe0016a220200
  Kernel stack location 0xffffd001f026a0c0 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a418 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a460 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a4d0 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a4f0 references THREAD 0xffffd001ee29cdc0
  Kernel stack location 0xffffd001f026a670 references THREAD 0xffffd001ee29cdc0


    ffffd001f026a0e0 nt!KiSwapContext+76
    ffffd001f026a190 nt!KiSwapThread+1c8
    ffffd001f026a220 nt!KiCommitThreadWait+148
    ffffd001f026a2e0 nt!KeWaitForMultipleObjects+21e
    ffffd001f026a800 nt!ObWaitForMultipleObjects+2b7
    ffffd001f026aa80 nt!NtWaitForMultipleObjects+f6
    000000c8d220fa98 nt!KiSystemServiceCopyEnd+13
    000000c8d220fa98 ntdll!ZwWaitForMultipleObjects+a
... 
```

 

 





