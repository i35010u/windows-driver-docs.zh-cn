---
title: 作业 (job)
description: 作业扩展显示作业对象。
keywords:
- 作业 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- job
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 62d01ea0993590db19d839dbedd4b7daf59bc5a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792041"
---
# <a name="job"></a>!job


**！作业** 扩展显示作业对象。

```dbgcmd
!job [Process [Flags]] 
```

## <a name="span-idddk__job_dbgspanspan-idddk__job_dbgspanparameters"></a><span id="ddk__job_dbg"></span><span id="DDK__JOB_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定进程或要检查其关联作业对象的线程的十六进制地址。 如果在 windows 2000) 中省略此项或等于-1 (，或在 Windows XP 和更高) 版本中等于零 (，则将显示与当前进程关联的作业。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定显示内容应包含的内容。 这可以是以下任一位值的总和。 默认值为0x1：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
使显示包括作业设置和统计信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使显示包含作业中所有进程的列表。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关作业对象的信息，请参阅 Russinovich 和 David 所罗门群岛上的 *Microsoft Windows 内部机制*。

<a name="remarks"></a>备注
-------

下面是此扩展的输出示例：

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

 

 





