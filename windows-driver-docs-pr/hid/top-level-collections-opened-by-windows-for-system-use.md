---
title: Windows 打开的供系统使用的顶级集合
description: Windows 打开的供系统使用的顶级集合
ms.assetid: e489ce46-379e-4ba9-a0e3-5848b1f4a17b
keywords:
- WDK HID 顶级集合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80f4c7794f4dada8b79d887a7b334539e40771f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384356"
---
# <a name="top-level-collections-opened-by-windows-for-system-use"></a>Windows 打开的供系统使用的顶级集合





Windows 将打开以下[顶级集合](top-level-collections.md)对于系统使用：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>设备类型</th>
<th>使用情况页面</th>
<th>使用 ID</th>
<th>Windows 客户端</th>
<th>访问模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>指针</p></td>
<td><p>0x01</p></td>
<td><p>0x01</p></td>
<td><p>Win32 子系统</p></td>
<td><p>独占</p></td>
</tr>
<tr class="even">
<td><p>鼠标</p></td>
<td><p>0x01</p></td>
<td><p>0x02</p></td>
<td><p>Win32 子系统</p></td>
<td><p>独占</p></td>
</tr>
<tr class="odd">
<td><p>游戏杆</p></td>
<td><p>0x01</p></td>
<td><p>0x04</p></td>
<td><p>DirectInput</p></td>
<td><p>共享</p></td>
</tr>
<tr class="even">
<td><p>游戏板</p></td>
<td><p>0x01</p></td>
<td><p>0x05</p></td>
<td><p>DirectInput</p></td>
<td><p>共享</p></td>
</tr>
<tr class="odd">
<td><p>键盘</p></td>
<td><p>0x01</p></td>
<td><p>0x06</p></td>
<td><p>Win32 子系统</p></td>
<td><p>独占</p></td>
</tr>
<tr class="even">
<td><p>键盘</p></td>
<td><p>0x01</p></td>
<td><p>0x07</p></td>
<td><p>Win32 子系统</p></td>
<td><p>独占</p></td>
</tr>
<tr class="odd">
<td><p>系统控制</p></td>
<td><p>0x01</p></td>
<td><p>0x80</p></td>
<td><p>Win32 子系统</p></td>
<td><p>共享</p></td>
</tr>
<tr class="even">
<td><p>使用者音频控件</p></td>
<td><p>0x0C</p></td>
<td><p>0x01</p></td>
<td><p>在 Windows 2000 和 Microsoft Windows XP 的 hidserv.dll （SVC 主机服务的一个） 输入 hidserv.exe</p></td>
<td><p>共享</p></td>
</tr>
</tbody>
</table>

 

 

 




