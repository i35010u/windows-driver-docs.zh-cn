---
title: Bug 检查 0xBD INVALID_HIBERNATED_STATE
description: INVALID_HIBERNATED_STATE bug 检查具有 0x000000BD 值。
ms.assetid: DB386A20-EE6F-4E2B-8FFD-51CCE0A8AEAC
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
ms.openlocfilehash: 71adbe71b1a18608fc6aab28e4796f935d5d9e4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562366"
---
# <a name="bug-check-0xbd-invalidhibernatedstate"></a>Bug 检查 0xBD：INVALID\_HIBERNATED\_STATE


无效\_HIBERNATED\_状态 bug 检查的值为 0x000000BD。 这表示休眠的内存映像与当前的硬件配置不匹配。 当系统从休眠状态恢复，并且发现硬件时系统已休眠已发生更改，将发生此错误检查。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="invalidhibernatedstate-parameters"></a>无效\_HIBERNATED\_状态参数


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
<td align="left"><p>无效的硬件。</p>
<p>1 :已安装的处理器数比以前少是休眠</p>
<p>参数 2 中的值：休眠状态前的处理器数</p>
<p>Param 3 中的值：后休眠的处理器数</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">每个参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">每个参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




