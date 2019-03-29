---
title: so（设置内核调试选项）
description: 因此，命令设置或显示内核调试选项。
ms.assetid: b40260c7-6e60-4198-988f-bcafecb165bc
keywords:
- 因此 （集内核调试选项） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- so (Set Kernel Debugging Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 331c83819a53e818e1dfb962224b3e6583025d05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563210"
---
# <a name="so-set-kernel-debugging-options"></a>so（设置内核调试选项）


**因此**命令设置或显示内核调试选项。

```dbgcmd
so [Options] 
```

## <a name="span-idddkcmdsetkerneldebuggingoptionsdbgspanspan-idddkcmdsetkerneldebuggingoptionsdbgspanparameters"></a><span id="ddk_cmd_set_kernel_debugging_options_dbg"></span><span id="DDK_CMD_SET_KERNEL_DEBUGGING_OPTIONS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
一个或多个以下选项：

<span id="NOEXTWARNING"></span><span id="noextwarning"></span>**NOEXTWARNING**  
调试器找不到扩展插件命令时不发出警告。

<span id="NOVERSIONCHECK"></span><span id="noversioncheck"></span>**NOVERSIONCHECK**  
不会检查调试器扩展 Dll 的版本。

如果省略*选项*，将显示当前选项。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

您还可以设置调试选项使用的内核\_NT\_调试\_选项[环境变量](kernel-mode-environment-variables.md)。

 

 





