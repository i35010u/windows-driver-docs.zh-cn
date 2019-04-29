---
title: 正在检查 IRP_MJ_READ 操作 Oplock 状态
description: 正在检查 IRP_MJ_READ 操作 Oplock 状态
ms.assetid: 9b4d1ba9-0838-44f1-8328-f60bfb3910ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4faf6bd530b129604bdf79e84b9e59f6d1e8d9bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324323"
---
# <a name="checking-the-oplock-state-of-an-irpmjread-operation"></a>正在检查 IRP_MJ_READ 操作 Oplock 状态


时，以下才适用*流*正在读取。 如果 TxF 事务处理读取器执行读取的因为事务处理读取器不包括编写器 （即编写器持有 oplock 根本不能同时存在），则不会进行此检查。
<table>
<tr>
<th>请求类型</th>
<th>条件</th>
</tr>
<tr>
<td rowspan="2">
<p>级别 1</p>
<p>Batch</p>
</td>
<td>
<p>IRP_MJ_READ 上中断时：</p>
<ul>
<li>
<p> 读取的操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断到级别 2。</p>
</li>
<li>
<p> 继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读写</p>
</td>
<td>
<p>IRP_MJ_READ 上中断时：</p>
<ul>
<li>
<p> 读取的操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断到读取。</p>
</li>
<li>
<p> 继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td rowspan="2">
<p>读写句柄</p>
</td>
<td>
<p>IRP_MJ_READ 上中断时：</p>
<ul>
<li>
<p> 读取的操作发生 FILE_OBJECT 具有不同 oplock 键 FILE_OBJECT 拥有 oplock。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>如果 oplock 已损坏：</p>
<ul>
<li>
<p> 中断到读取句柄。</p>
</li>
<li>
<p> 继续操作之前必须收到确认。</p>
</li>
</ul>
</td>
</tr>
<tr>
<td>
<p>级别 2</p>
<p>Filter</p>
<p>Read</p>
<p>读取句柄</p>
</td>
<td>
<ul>
<li>
<p> 就不会破坏 oplock，不发送任何确认是必需的可以立即继续操作。</p>
</li>
</ul>
</td>
</tr>
</table>

 




