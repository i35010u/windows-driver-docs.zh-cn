---
title: 远程 NDIS 文件命名约定
description: 远程 NDIS 文件命名约定
keywords:
- 远程 NDIS WDK 网络，驱动程序名称
- 远程 NDIS WDK 网络，操作系统支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8fe6b7ae31099799de35802fa05e555cf3b8d4a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836297"
---
# <a name="remote-ndis-file-naming-conventions"></a>远程 NDIS 文件命名约定





为了支持旧版远程 NDIS 设备，Windows 的各个版本中都包含了多个远程 NDIS 驱动程序。 下表列出了每个版本的 Windows 中使用的远程 NDIS 驱动程序名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">远程 NDIS 文件名</th>
<th align="left">提供此驱动程序的 Windows 版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Rndismp.sys Usb8023.sys</p></td>
<td align="left"><p>这些二进制文件仅提供给旧设备支持。 远程 NDIS 设备 INF 文件不应引用这些驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rndismpy.sys Usb8023y.sys</p></td>
<td align="left"><p>Windows 2000。 与操作系统分开提供。 这些是 Microsoft 授予重新分发权限的唯一二进制文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rndismpx.sys Usb8023x.sys Netrndis</p></td>
<td align="left"><ul>
<li><p>Windows XP SP2 及更高版本</p></li>
<li><p>Windows XP x64</p></li>
<li><p>Windows Server 2003 SP1 (x86、x64、ia64) 和更高版本</p></li>
<li><p>Windows Vista (x86、x64) 和更高版本</p></li>
</ul>
<p>Rndismpx.sys 和 Usb8023x.sys 二进制文件是操作系统的一部分。 Netrndis 文件是操作系统的一部分的内部文件。 所有这些文件都必须由由 IHV 提供的 INF 文件引用，如 <a href="remote-ndis-inf-template.md" data-raw-source="[Remote NDIS INF Template](remote-ndis-inf-template.md)">远程 NDIS Inf 模板</a>中所述。</p></td>
</tr>
</tbody>
</table>

 

**注意**  Windows 98/Me/SE 或以前的版本不支持远程 NDIS。

 

 

 





