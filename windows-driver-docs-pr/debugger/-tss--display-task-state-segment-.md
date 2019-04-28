---
title: .tss（显示任务状态段）
description: .Tss 命令显示当前处理器的已保存任务状态段 (/{TSS) 信息的格式化的视图。
ms.assetid: 3f73b7cf-56a8-434a-bc4d-2e8ab3af9f94
keywords:
- 显示任务状态段 (.tss) 命令
- 任务状态段 (/{TSS)
- /{TSS （任务状态段）
- .tss （显示任务状态段） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .tss (Display Task State Segment)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66f233b2fea635695b7403e3c2a1851b71ba9852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334171"
---
# <a name="tss-display-task-state-segment"></a>.tss（显示任务状态段）


**.Tss**命令显示当前处理器的已保存任务状态段 (/{TSS) 信息的格式化的视图。

```dbgcmd
.tss [Address]
```

## <a name="span-idddkmetadisplaytaskstatesegmentdbgspanspan-idddkmetadisplaytaskstatesegmentdbgspanparameters"></a><span id="ddk_meta_display_task_state_segment_dbg"></span><span id="DDK_META_DISPLAY_TASK_STATE_SEGMENT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
/{TSS 的地址。

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
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅限 x86</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以通过检查的输出中找到的 /{TSS 地址[ **！ pcr** ](-pcr.md)扩展。

 

 





