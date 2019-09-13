---
title: Bug 检查 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
description: VIDEO_SCHEDULER_INTERNAL_ERROR bug 检查的值为0x00000119。 这表示视频计划程序检测到严重冲突。
ms.assetid: dfffdd70-c519-4e39-a604-a0ba2217093b
keywords:
- Bug 检查 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
- VIDEO_SCHEDULER_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_SCHEDULER_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ecc3c1adaeb8f3956a0a5f19c4efb14646a1e1d
ms.sourcegitcommit: 3405003dfd52682948f569253099545d8f9513ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70912721"
---
# <a name="bug-check-0x119-video_scheduler_internal_error"></a>Bug 检查 0x119：视频\_计划\_程序内部\_错误


视频\_计划程序\_内部\_错误检查的值为0x00000119。 这表示视频计划程序检测到严重冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户, 请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_scheduler_internal_error-parameters"></a>视频\_计划\_程序内部\_错误参数


参数1是唯一相关的参数，用于标识完全冲突。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数1</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>驱动程序报告了无效的防护 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>提交命令时驱动程序失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>驱动程序在修补命令缓冲区时失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>驱动程序报告了无效的翻转功能。</p></td>
</tr>
</tbody>
</table>

 
## <a name="resolution"></a>分辨率

[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 




