---
title: .tss（显示任务状态段）
description: Tss 命令显示当前处理器的已保存任务状态段 (TSS) 信息的格式化视图。
keywords:
- " () 命令显示任务状态段"
- '任务状态段 (TSS) '
- 'TSS (任务状态段) '
- tss (显示任务状态段) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .tss (Display Task State Segment)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80226c0edbae2ef911def739c4dc379425ca9a68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829985"
---
# <a name="tss-display-task-state-segment"></a>.tss（显示任务状态段）


**Tss** 命令显示当前处理器的已保存任务状态段 (tss) 信息的格式化视图。

```dbgcmd
.tss [Address]
```

## <a name="span-idddk_meta_display_task_state_segment_dbgspanspan-idddk_meta_display_task_state_segment_dbgspanparameters"></a><span id="ddk_meta_display_task_state_segment_dbg"></span><span id="DDK_META_DISPLAY_TASK_STATE_SEGMENT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
TSS 的地址。

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
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅限 x86</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

通过检查 [**！ pcr**](-pcr.md) 扩展的输出，可以找到 TSS 的地址。

 

 





