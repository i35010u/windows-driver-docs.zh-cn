---
title: Bug 检查 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
description: VIDEO_SCHEDULER_INTERNAL_ERROR bug 检查具有 0x00000119 值。 这表示视频的计划程序已检测到严重冲突。
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
ms.openlocfilehash: 1702af363ee3049d518b5d08a172abe5efed48ab
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238398"
---
# <a name="bug-check-0x119-videoschedulerinternalerror"></a>Bug 检查 0x119：VIDEO\_SCHEDULER\_INTERNAL\_ERROR


视频\_计划程序\_内部\_错误 bug 检查的值为 0x00000119。 这表示视频的计划程序已检测到严重冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="videoschedulerinternalerror-parameters"></a>视频\_计划程序\_内部\_错误参数


参数 1 是感兴趣的唯一参数，并标识了确切的冲突。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>该驱动程序报告了无效的隔离 id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>命令的提交后，该驱动程序失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>此驱动程序失败时修补命令缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>该驱动程序报告了无效的翻页功能。</p></td>
</tr>
</tbody>
</table>

 

 

 




