---
title: 正在检查 IRP_MJ_WRITE 操作 Oplock 状态
description: 正在检查 IRP_MJ_WRITE 操作 Oplock 状态
ms.assetid: 04d09810-f157-4140-8bfb-c780a65cdf77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0933098d31497029f47e57097b9a646def7e60e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324277"
---
# <a name="checking-the-oplock-state-of-an-irpmjwrite-operation"></a>正在检查 IRP_MJ_WRITE 操作 Oplock 状态


时，以下才适用*流*是写入和写入不是分页 I/O。

<table>
<tr>
<th>请求类型</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>级别 1</p>
<p>Batch</p>
<p>Filter</p>
<p>读取句柄</p>
<p>读写</p>
<p>读写句柄</p>
</td>
<td>
<p>IRP_MJ_WRITE 上中断时：</p>
<ul>
<li>
<p> 写入操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断为无。</p>
</li>
<li>
<p> 读取句柄请求：尽管需要确认该中断，则操作将继续立即 （例如，而无需等待确认）。</p>
</li>
<li>
<p> 对于所有其他请求类型：继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>Read</p>
</td>
<td>
<p>IRP_MJ_WRITE 上中断时：</p>
<ul>
<li>
<p> 写入操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断为无。</p>
</li>
<li>
<p> 不发送任何确认是必需的可以立即继续操作。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>级别 2</p>
</td>
<td>
<ul>
<li>
<p> 为无始终中断。</p>
</li>
<li>
<p> 不发送任何确认是必需的可以立即继续操作。</p>
</li>
</ul>
</td>
</tr>
</table>
 

 




