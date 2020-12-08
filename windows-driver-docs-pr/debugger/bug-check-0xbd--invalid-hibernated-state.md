---
title: Bug 检查 0xBD INVALID_HIBERNATED_STATE
description: INVALID_HIBERNATED_STATE bug 检查的值为0x000000BD。
keywords:
- Bug 检查 0xBD INVALID_HIBERNATED_STATE
- INVALID_HIBERNATED_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_HIBERNATED_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a29fef9b23558a77b31c1f0ebc3f95a32a490869
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783547"
---
# <a name="bug-check-0xbd-invalid_hibernated_state"></a>Bug 检查0xBD：无效的 \_ 休眠 \_ 状态


无效的 \_ 休眠 \_ 状态 bug 检查的值为0x000000BD。 这表明休眠的内存映像与当前硬件配置不匹配。 当系统从休眠状态恢复，并发现在系统休眠时硬件发生了更改时，会发生此错误检测。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_hibernated_state-parameters"></a>无效的 \_ 休眠 \_ 状态参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>硬件无效。</p>
<p>1：已安装的处理器数小于休眠之前</p>
<p>Param 2 中的值：休眠之前的处理器数</p>
<p>参数3中的值：休眠后的处理器数</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">每个参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">每个参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




