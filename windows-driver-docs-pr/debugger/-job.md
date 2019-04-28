---
title: 作业
description: 作业扩展显示作业对象。
ms.assetid: 1fbadcc7-d81b-4cfb-a54a-7843e2f78ea1
keywords:
- Windows 调试作业
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- job
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6bf7d630b4f0d5367147d1f3d6a18c93a4b3a7ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336336"
---
# <a name="job"></a>!job


**！ 作业**扩展显示作业对象。

```dbgcmd
!job [Process [Flags]] 
```

## <a name="span-idddkjobdbgspanspan-idddkjobdbgspanparameters"></a><span id="ddk__job_dbg"></span><span id="DDK__JOB_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定的进程或线程的关联的作业对象是要检查其十六进制的地址。 如果省略此属性，或者为-1 （在 Windows 2000 中)，等同于或等于零 （在 Windows XP 及更高版本），与当前进程关联的作业将显示。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定显示应包含的内容。 这可以是任何以下位值的总和。 默认值为 0x1:

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括作业设置和统计信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示效果以包括在作业中的所有进程的列表。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

作业对象的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

下面是输出的来自此扩展插件示例：

```dbgcmd
kd> !process 52c
Searching for Process with Cid == 52c
PROCESS 8276c550  SessionId: 0  Cid: 052c    Peb: 7ffdf000  ParentCid: 0060
    DirBase: 01289000  ObjectTable: 825f0368  TableSize:  24.
    Image: cmd.exe
    VadRoot 825609e8 Vads 30 Clone 0 Private 77. Modified 0. Locked 0.
    DeviceMap e1733f38
    Token                             e1681610
    ElapsedTime                       0:00:12.0949
    UserTime                          0:00:00.0359
    .....
    CommitCharge                      109
    Job                               8256e1f0

kd> !job 8256e1f0
Job at ffffffff8256e1f0
  TotalPageFaultCount      0
  TotalProcesses           1
  ActiveProcesses          1
  TotalTerminatedProcesses 0
  LimitFlags               0
  MinimumWorkingSetSize    0
  MaximumWorkingSetSize    0
  ActiveProcessLimit       0
  PriorityClass            0
  UIRestrictionsClass      0
  SecurityLimitFlags       0
  Token                    00000000
```

 

 





