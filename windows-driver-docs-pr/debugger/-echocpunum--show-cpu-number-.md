---
title: .echocpunum（显示 CPU 数目）
description: .Echocpunum 命令打开或关闭调试多处理器的目标计算机时显示的处理器数。
ms.assetid: a238b291-8c6e-4a4c-adc3-3be5a9916a29
keywords:
- 显示 CPU 数量 (.echocpunum) 命令
- 显示 CPU 数量 (.echocpunum) 命令的多处理器计算机
- .echocpunum （显示 CPU 数） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echocpunum (Show CPU Number)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fead002bd508311910785e453d4e3ab067cd2c62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336799"
---
# <a name="echocpunum-show-cpu-number"></a>.echocpunum（显示 CPU 数目）


**.Echocpunum**命令打开或关闭调试多处理器的目标计算机时显示的处理器数。

```dbgcmd
.echocpunum 0 
.echocpunum 1 
.echocpunum 
```

## <a name="span-idddkmetashowcpunumberdbgspanspan-idddkmetashowcpunumberdbgspanparameters"></a><span id="ddk_meta_show_cpu_number_dbg"></span><span id="DDK_META_SHOW_CPU_NUMBER_DBG"></span>参数


<span id="_______0______"></span> **0**   
关闭显示器的处理器数。

<span id="_______1______"></span> **1**   
打开显示的处理器数。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何调试多处理器计算机的详细信息，请参阅[多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

如果您使用 **.echocpunum**命令不带任何参数的处理器编号显示已启用还是已关闭，并显示新状态。

默认情况下处于关闭状态显示。

 

 





