---
title: 远程 NDIS 文件命名约定
description: 远程 NDIS 文件命名约定
ms.assetid: 9c5b2cfe-c38f-4314-a91c-f27c77ea1f63
keywords:
- 远程 NDIS WDK 网络、 驱动程序名称
- 远程 NDIS WDK 网络、 操作系统支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e82f1ad42a769675ad313e38324466e2c45e210b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547441"
---
# <a name="remote-ndis-file-naming-conventions"></a>远程 NDIS 文件命名约定





为了支持旧远程 NDIS 设备，多个远程 NDIS 驱动程序包含了各种版本的 Windows。 下表列出了每个版本的 Windows 中使用的远程 NDIS 驱动程序名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">远程 NDIS 文件名称</th>
<th align="left">此驱动程序位于 Windows 版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Rndismp.sys Usb8023.sys</p></td>
<td align="left"><p>仅对旧设备支持的传送这些二进制文件。 没有远程 NDIS 设备 INF 文件应该引用这些驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Rndismpy.sys Usb8023y.sys</p></td>
<td align="left"><p>Windows 2000。 从操作系统单独提供。 这些是 Microsoft 为其授予重新分发权限的唯一二进制文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Rndismpx.sys Usb8023x.sys Netrndis.inf</p></td>
<td align="left"><ul>
<li><p>Windows XP SP2 及更高版本</p></li>
<li><p>Windows XP x64</p></li>
<li><p>Windows Server 2003 SP1 （x86、 x64、 ia64） 及更高版本</p></li>
<li><p>Windows Vista （x86、 x64） 及更高版本</p></li>
</ul>
<p>作为操作系统的一部分提供 Rndismpx.sys 和 Usb8023x.sys 二进制文件。 Netrndis.inf 文件是操作系统的一部分的内部文件。 所有这些文件必须引用由 IHV 提供 INF 文件中所述<a href="remote-ndis-inf-template.md" data-raw-source="[Remote NDIS INF Template](remote-ndis-inf-template.md)">远程 NDIS INF 模板</a>。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  远程 NDIS 不支持在 Windows 98/我/SE 或以前的版本。

 

 

 





