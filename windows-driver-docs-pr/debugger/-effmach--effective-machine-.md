---
title: .effmach（有效计算机）
description: .Effmach 命令显示或更改调试器使用的处理器模式。
ms.assetid: bf4dfdc0-2f0b-416a-8bf2-0e7d81339905
keywords:
- 有效的计算机 (.effmach) 命令
- .effmach （有效的机器） Windows 调试
ms.date: 01/24/2018
topic_type:
- apiref
api_name:
- .effmach (Effective Machine)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 65bf2b32e2b783f49eb841f9068a1a58ff48236b
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349828"
---
# <a name="effmach-effective-machine"></a>.effmach（有效计算机）


**.Effmach**命令显示或更改调试器使用的处理器模式。

```dbgcmd
.effmach [MachineType]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______MachineType______"></span><span id="_______machinetype______"></span><span id="_______MACHINETYPE______"></span> *MachineType*   
指定调试器使用此会话的处理器类型。 如果省略此参数时，调试器会显示当前的计算机类型。

您可以输入以下计算机类型之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>计算机类型</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.</strong></p></td>
<td align="left"><p>使用目标计算机的本机处理器模式下的处理器模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>使用正在执行的代码处理器模式下进行的最新事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>x86</strong></p></td>
<td align="left"><p>使用基于 x86 的处理器模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>amd64</strong></p></td>
<td align="left"><p>使用基于 x64 的处理器模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ebc</strong></p></td>
<td align="left"><p>使用 EFI 字节代码处理器模式。</p></td>
</tr>
</tr>
<tr class="odd">
<td align="left"><p><strong>arm</strong></p></td>
<td align="left"><p>使用 ARM64 处理器模式。</p></td>
</tr>
</tr>
<tr class="evenodd">
<td align="left"><p><strong>chpe</strong></p></td>
<td align="left"><p>使用 CHPE 处理器模式。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

处理器模式下会影响许多调试器功能：

-   哪些处理器用于堆栈跟踪。

-   是否在过程使用 32 位或 64 位指针。

-   哪些处理器的注册组处于活动状态。

 

 





