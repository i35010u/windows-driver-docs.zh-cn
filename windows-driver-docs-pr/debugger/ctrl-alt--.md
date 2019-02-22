---
title: CTRL + ALT + \ （调试当前调试器）
description: CTRL + ALT + \ 键组合启动 CDB; 的新实例此新调试器将当前的调试器作为其目标。
ms.assetid: 0a36baa4-fe40-4498-9cf8-ae81497f1dda
keywords:
- CTRL + ALT + （调试当前调试器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+ALT+\ (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de0743fec4ff83632b8a67676265b0797dbb866b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523175"
---
# <a name="ctrlalt-debug-current-debugger"></a>CTRL + ALT +\\ （调试当前调试器）


**CTRL + ALT +\\** 密钥启动 CDB 的新实例; 此新的调试程序会为其目标为当前的调试器。

```dbgcmd
CTRL+ALT+\ 
```

## <span id="ddk_meta_ctrl_p_dbg"></span><span id="DDK_META_CTRL_P_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>调试器</strong></td>
<td align="left"><p>WinDbg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

这相当于启动通过新 CDB [ **remote.exe** ](the-remote-exe-utility.md)实用程序，并使用它进行调试的调试程序已运行。

**CTRL + ALT +\\** 类似于[ **.dbgdbg （调试当前调试器）** ](-dbgdbg--debug-current-debugger-.md)命令，但是**CTRL + ALT +\\** 具有优势，可以在没有调试程序命令行可用时。

 

 





