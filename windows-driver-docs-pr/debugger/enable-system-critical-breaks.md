---
title: 启用系统关键突破
description: 启用系统关键突破
keywords:
- '启用系统严重中断 (全局标志) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 968aad9b6bf91e7b0468c5631330c08e4123304f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838229"
---
# <a name="enable-system-critical-breaks"></a>启用系统关键突破


## <span id="ddk_enable_system_critical_breaks_dtools"></span><span id="DDK_ENABLE_SYSTEM_CRITICAL_BREAKS_DTOOLS"></span>


**启用系统严重中断** 标志会强制系统中断调试器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>scb</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x100000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_ENABLE_SYSTEM_CRIT_BREAKS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

为进程 (图像文件) 设置时，如果指定的进程异常停止，此标志会强制系统中断到调试器。 仅当进程调用 **RtlSetProcessBreakOnExit** 和 **RtlSetThreadBreakOnExit** 接口时，此标志才有效。

当设置系统范围 (注册表或内核标记) 时，无论调用 **RtlSetProcessBreakOnExit** 和 **RtlSetThreadBreakOnExit** 接口的进程异常停止，此标志都会强制系统中断到调试器。

 

 





