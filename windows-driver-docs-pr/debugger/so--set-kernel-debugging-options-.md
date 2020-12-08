---
title: so（设置内核调试选项）
description: So 命令设置或显示内核调试选项。
keywords:
- 因此 (设置) Windows 调试的内核调试选项
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- so (Set Kernel Debugging Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 973e931954b6bce0709df6a8fd2667263b6bdb51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838355"
---
# <a name="so-set-kernel-debugging-options"></a>so（设置内核调试选项）


**So** 命令设置或显示内核调试选项。

```dbgcmd
so [Options] 
```

## <a name="span-idddk_cmd_set_kernel_debugging_options_dbgspanspan-idddk_cmd_set_kernel_debugging_options_dbgspanparameters"></a><span id="ddk_cmd_set_kernel_debugging_options_dbg"></span><span id="DDK_CMD_SET_KERNEL_DEBUGGING_OPTIONS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下一个或多个选项：

<span id="NOEXTWARNING"></span><span id="noextwarning"></span>**NOEXTWARNING**  
如果调试器找不到扩展命令，则不会发出警告。

<span id="NOVERSIONCHECK"></span><span id="noversioncheck"></span>**NOVERSIONCHECK**  
不检查调试器扩展 Dll 的版本。

如果省略 *选项*，则显示当前选项。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

你还可以使用 \_ NT \_ 调试 \_ 选项 [环境变量](kernel-mode-environment-variables.md)来设置内核调试选项。

 

 





