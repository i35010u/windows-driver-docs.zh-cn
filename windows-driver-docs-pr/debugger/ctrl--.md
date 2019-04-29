---
title: CTRL+\（调试当前调试器）
description: CTRL + \ 键组合启动 CDB; 的新实例此新调试器将当前的调试器作为其目标。
ms.assetid: c0c63af5-712c-47b6-8811-81e441ddb3df
keywords:
- CTRL + （调试当前调试器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+\ (Debug Current Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f377f5f248a0ea1d0a623f71b011d3dba8d7dc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374977"
---
# <a name="ctrl-debug-current-debugger"></a>CTRL +\\ （调试当前调试器）


**CTRL +\\** 密钥启动 CDB 的新实例; 此新的调试程序会为其目标为当前的调试器。

```dbgcmd
CTRL+\  ENTER 
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
<td align="left"><p>CDB、 NTSD，KD</p></td>
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

[**CTRL +\\**  ](ctrl-alt--.md)类似于[ **.dbgdbg （调试当前调试器）** ](-dbgdbg--debug-current-debugger-.md)命令。

 

 





