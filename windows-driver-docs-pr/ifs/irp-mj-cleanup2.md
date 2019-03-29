---
title: 正在检查 IRP_MJ_CLEANUP 操作 Oplock 状态
description: 正在检查 IRP_MJ_CLEANUP 操作 Oplock 状态
ms.assetid: 5e078575-cbb8-4460-9986-4c546b8c20be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2b8e6065d57a947162f4a893ff64bdef81416d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562170"
---
# <a name="checking-the-oplock-state-of-an-irpmjcleanup-operation"></a>正在检查 IRP_MJ_CLEANUP 操作 Oplock 状态


时，以下才适用*流*正在关闭。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">请求类型</th>
<th align="left">条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>级别 1</p>
<p>Batch</p>
<p>Filter</p>
<p>读取句柄</p>
<p>读写</p>
<p>读写句柄</p></td>
<td align="left"><ul>
<li><p>为无始终中断。</p></li>
<li><p>不发送任何确认是必需的可以立即继续操作。 请注意，等待来自挂起的分行符请求确认任何 I/O 操作 (Irp) 立即完成。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>级别 2</p>
<p>Read</p></td>
<td align="left"><ul>
<li><p>为无始终中断。 请注意，不会影响同一个流其他级别 2 或读取 oplock;仅与此 FILE_OBJECT 关联级别 2 或读取 oplock 已断开。</p></li>
<li><p>不发送任何确认是必需的可以立即继续操作。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

 

 




