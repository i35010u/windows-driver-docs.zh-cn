---
title: .record_branches（启用分支记录）
description: .Record_branches 命令启用目标代码执行的分支记录。
keywords:
- " ( .record_branches) 命令启用分支记录"
- .record_branches (在 Windows 调试) 启用分支记录
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .record_branches (Enable Branch Recording)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2057fdd6910dc932f84db152cd0872178fa01598
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815491"
---
# <a name="record_branches-enable-branch-recording"></a>。记录 \_ 分支 (启用分支记录) 


" **记录 \_ 分支** " 命令启用目标代码执行的分支记录。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>仅基于 x64</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

通过 " **记录 \_ 分支 1** " 命令，可以在目标的代码中记录分支。 " **记录 \_ 分支 0** " 命令禁用此记录。

如果没有参数，则 **。记录 \_ 分支** 显示此设置的当前状态。

 

 





