---
title: 调试静态图像组件
description: 调试静态图像组件
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 397c232716907ce470675a267eb12978166acd39
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832975"
---
# <a name="debugging-still-image-components"></a>调试静态图像组件

为了帮助调试供应商提供的静止图像组件，可以使用 "**开始**" 菜单的 "**运行**" 选项，使用命令行选项来修改静态图像事件监视器的行为。 可以使用以下选项：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>命令行选项</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>stimon/h</strong></p></td>
<td><p>隐藏消息窗口。</p></td>
</tr>
<tr class="even">
<td><p><strong>Stimon/r</strong></p></td>
<td><p>刷新事件监视器的设备列表。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Stimon/t</strong><em>number</em></p></td>
<td><p>将轮询间隔修改为按 <em>number</em>指定的秒数。 通常用于提高轮询间隔。</p></td>
</tr>
<tr class="even">
<td><p><strong>Stimon/v</strong></p></td>
<td><p>使显示事件监视器消息的窗口可见。</p></td>
</tr>
</tbody>
</table>

可以使用 "计算机管理" 窗口停止并启动事件监视器。 事件监视器作为 "静止图像服务" 列出。
