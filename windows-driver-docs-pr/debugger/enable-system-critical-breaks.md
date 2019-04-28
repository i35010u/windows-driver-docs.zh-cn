---
title: 启用系统关键突破
description: 启用系统关键突破
ms.assetid: f13372b9-604e-4ea5-96e2-d8b7e916c8e5
keywords:
- 启用系统关键分隔线 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c6da80674db36165f0ac1fac4333b43d72c489
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340606"
---
# <a name="enable-system-critical-breaks"></a>启用系统关键突破


## <span id="ddk_enable_system_critical_breaks_dtools"></span><span id="DDK_ENABLE_SYSTEM_CRITICAL_BREAKS_DTOOLS"></span>


**启用系统关键的分隔线**标志会强制系统中断到调试器。

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
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果设置为进程 （图像文件），此标志会强制系统中断到调试器只要指定的进程异常停止。 此标志仅当在过程调用是有效**RtlSetProcessBreakOnExit**并**RtlSetThreadBreakOnExit**接口。

当系统级设置 （注册表或内核标志），此标志会强制系统中断到调试器时进程具有名为**RtlSetProcessBreakOnExit**和**RtlSetThreadBreakOnExit**接口异常停止。

 

 





