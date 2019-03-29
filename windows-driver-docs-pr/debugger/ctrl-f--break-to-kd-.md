---
title: CTRL+F（中断到 KD）
description: CTRL + F 键取消命令，或进入调试器。
ms.assetid: 45bb7eaf-cb79-4fb4-a01d-373bfb1957c3
keywords:
- CTRL + F （中断添加到 KD） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+F (Break to KD)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d35629ef83e832fa147661431be722ed065d9195
ms.sourcegitcommit: 55dfaaca86e07bef7c41fe601e67cbba1b56ef15
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58505149"
---
# <a name="ctrlf-break-to-kd"></a>CTRL+F（中断到 KD）


CTRL + F 键取消命令，或进入调试器。 （此控制密钥是特别有用使用 CDB 调试 KD 自身时。）

```dbgcmd
CTRL+F  ENTER 
```


## <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>调试器</strong></p></td>
<td align="left"><p>CDB KD</p></td>
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

通常情况下，按 CTRL + F 等同于标准中断命令 ([**CTRL + C** ](ctrl-c--break-.md) KD 和 CDB 和[调试 |中断](debug---break.md)或 CTRL + BREAK 在 WinDbg 中。)

但是，如果你正在调试使用 CDB KD，这两个密钥将以不同的方式工作。 CTRL + C 将截获主机调试器 (CDB) 时按 CTRL + F 将截获由目标调试器 (KD)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**.breakin （中断添加到内核调试程序）**](-breakin--break-to-the-kernel-debugger-.md)

 

 






