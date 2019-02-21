---
title: .record_branches （启用分支录制）
description: .Record_branches 命令启用目标的代码执行的分支的记录。
ms.assetid: 522eeba5-b6c5-473c-9c8e-8ef4c941079f
keywords:
- 启用分支录制 (.record_branches) 命令
- .record_branches （启用分支录制） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .record_branches (Enable Branch Recording)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f06ce24825ac7170f226347d2477d55af9aa6720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526485"
---
# <a name="recordbranches-enable-branch-recording"></a>.record\_分支 （启用分支录制）


**.Record\_分支**命令启用目标的代码执行的分支的记录。

```dbgcmd
.record_branches {1|0} 
.record_branches
```

## <span id="ddk_meta_enable_branch_recording_dbg"></span><span id="DDK_META_ENABLE_BRANCH_RECORDING_DBG"></span>


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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>基于 x64 的仅</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Record\_分支 1**命令启用目标的代码中的分支的记录。 **.Record\_分支 0**命令将禁用此记录。

不带参数， **.record\_分支**显示此设置的当前状态。

 

 





