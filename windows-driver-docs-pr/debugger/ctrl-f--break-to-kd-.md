---
title: CTRL+F（中断到 KD）
description: CTRL + F 键取消命令或中断调试器。
keywords:
- CTRL + F (中断到 KD) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+F (Break to KD)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 234e4a47f8714305334cd77541b23b3ae2185fd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787005"
---
# <a name="ctrlf-break-to-kd"></a>CTRL+F（中断到 KD）


CTRL + F 键取消命令或中断调试器。  (当使用 CDB 调试 KD 本身时，此控制键特别有用。 ) 

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
<td align="left"><p>CDB，KD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在典型条件下，CTRL + F 与 KD 和 CDB 中 ([**ctrl + C**](ctrl-c--break-.md) 的标准 break 命令和 [Debug |](debug---break.md) ) 中的 break 或 CTRL + break

但是，如果正在使用 CDB 调试 KD，则这两个密钥的工作方式有所不同。 CTRL + C 将被宿主调试器截获 (CDB) ，而 CTRL + F 将被目标调试器截获 (KD) 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**.breakin（突入内核调试程序）**](-breakin--break-to-the-kernel-debugger-.md)

 

 






