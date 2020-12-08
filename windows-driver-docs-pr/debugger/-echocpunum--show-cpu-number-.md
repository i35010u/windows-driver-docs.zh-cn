---
title: .echocpunum（显示 CPU 数目）
description: 调试多处理器目标计算机时，echocpunum 命令将打开或关闭处理器编号的显示。
keywords:
- " ( 显示 CPU 号) 命令"
- 多处理器计算机， ( 中显示 CPU 号) 命令
- echocpunum (显示 CPU 号) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echocpunum (Show CPU Number)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6061faaf8c9e3e06c89f715ae213522e5e3138b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817915"
---
# <a name="echocpunum-show-cpu-number"></a>.echocpunum（显示 CPU 数目）


调试多处理器目标计算机时， **echocpunum** 命令将打开或关闭处理器编号的显示。

```dbgcmd
.echocpunum 0 
.echocpunum 1 
.echocpunum 
```

## <a name="span-idddk_meta_show_cpu_number_dbgspanspan-idddk_meta_show_cpu_number_dbgspanparameters"></a><span id="ddk_meta_show_cpu_number_dbg"></span><span id="DDK_META_SHOW_CPU_NUMBER_DBG"></span>参数


<span id="_______0______"></span>**0**   
关闭处理器编号的显示。

<span id="_______1______"></span>**1**   
打开处理器编号的显示。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何调试多处理器计算机的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

如果使用不带任何参数的 **echocpunum** 命令，则将打开或关闭处理器编号的显示，并显示新状态。

默认情况下，显示已关闭。

 

 





