---
title: Bug 检查 0x106 AGP_ILLEGALLY_REPROGRAMMED
description: AGP_ILLEGALLY_REPROGRAMMED bug 检查具有 0x00000106 值。 这表示加速图形端口 (AGP) 硬件，已囿通过未经授权的代理。
ms.assetid: 7acccf9b-bc4f-4842-a332-1023ab26f03d
keywords:
- Bug 检查 0x106 AGP_ILLEGALLY_REPROGRAMMED
- AGP_ILLEGALLY_REPROGRAMMED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_ILLEGALLY_REPROGRAMMED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 071a8fa6b22858253a001c0cb72a81f77d4e58cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533781"
---
# <a name="bug-check-0x106-agpillegallyreprogrammed"></a>Bug 检查 0x106:AGP\_非法\_REPROGRAMMED


AGP\_非法\_REPROGRAMMED bug 检查的值为 0x00000106。 这表示加速图形端口 (AGP) 硬件，已囿通过未经授权的代理。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="agpillegallyreprogrammed-parameters"></a>AGP\_非法\_REPROGRAMMED 参数


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
<td align="left"><p>1</p></td>
<td align="left"><p>最初通过编程方式设置的 AGP 命令注册值</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>当前命令寄存器值</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

无符号整数，或未正确测试视频，通常会出现此 bug 检查驱动程序。

<a name="resolution"></a>分辨率
----------

查看更新后的显示驱动程序的视频制造商的网站或使用 VGA 模式。

 

 




