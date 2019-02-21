---
title: 正在检查 IRP_MJ_LOCK_CONTROL 操作 Oplock 状态
description: 正在检查 IRP_MJ_LOCK_CONTROL 操作 Oplock 状态
ms.assetid: 6e0a5287-9a22-465f-b345-c9af556e6cdb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf870352b31e9e894d07f60cd8c3ba9aec8562cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525628"
---
# <a name="checking-the-oplock-state-of-an-irpmjlockcontrol-operation"></a>正在检查 IRP_MJ_LOCK_CONTROL 操作 Oplock 状态


以下应用给定的流上每个字节范围锁定操作。
<table>
<tr>
<th>请求类型</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>级别 1</p>
<p>Batch</p>
<p>读取句柄</p>
<p>读写</p>
<p>读写句柄</p>
</td>
<td>
<p>IRP_MJ_LOCK_CONTROL 上中断时：</p>
<ul>
<li>
<p> 锁定操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
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
<p>句柄请求：尽管需要确认该中断，则操作将继续立即 （例如，而无需等待确认）。</p>
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
<p>IIRP_MJ_LOCK_CONTROL 上中断时：</p>
<ul>
<li>
<p> 锁定操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
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
<p>Filter</p>
</td>
<td>
<ul>
<li>
<p> 就不会破坏 oplock，不发送任何确认是必需的可以立即继续操作。</p>
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

 

 




