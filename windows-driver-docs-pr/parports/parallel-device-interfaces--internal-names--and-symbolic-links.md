---
title: 并行设备接口、内部名称和符号链接
description: 并行设备接口、内部名称和符号链接
keywords:
- 系统提供的并行驱动程序 WDK，设备接口
- 系统提供的并行驱动程序 WDK，内部名称
- 系统提供的并行驱动程序 WDK、符号链接
- 设备接口 WDK 并行驱动程序
- 符号链接 WDK 并行驱动程序
- 内部名称 WDK 并行驱动程序
- 命名 WDK 并行驱动程序
- 未受保护的符号链接 WDK
- 并行设备 WDK，设备接口
- 设备对象 WDK 并行驱动程序
- 并行设备 WDK，内部名称
- 并行设备 WDK，符号链接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b16479564d43c09b32f9fac5a1d5a071eb261d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812585"
---
# <a name="parallel-device-interfaces-internal-names-and-symbolic-links"></a>并行设备接口、内部名称和符号链接





本部分介绍系统提供的并行端口和设备连接到并行端口的并行驱动程序创建的设备接口、内部名称和符号链接。

对于系统中枚举的每个并行端口和在并行端口上枚举的每个并行设备，并行驱动程序将创建设备对象、接口、内部名称和未受保护的符号链接，如下所示。

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
<th>设备对象</th>
<th>设备接口</th>
<th>内部名称</th>
<th>符号链接</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>并行端口</p></td>
<td><p>FDO</p></td>
<td><p>GUID_PARALLEL_DEVICE</p></td>
<td><p>"\Device\ParallelPort<em>m"，</em></p>
<p><em> &gt; m = </em> 0</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>原始并行设备</p></td>
<td><p>PDO</p></td>
<td><p>GUID_PARCLASS_DEVICE</p></td>
<td><p>"\Device\Parallel<em>m</em>"，</p>
<p><em> &gt; m = </em> 0</p></td>
<td><p>"LPT<em>n</em>"，</p>
<p><em>n = m +</em> 1</p></td>
</tr>
<tr class="odd">
<td><p>IEEE 1284.3 设备</p></td>
<td><p>PDO</p></td>
<td><p>无</p></td>
<td><p>"\Device\Parallel：<em>x</em>"，</p>
<p><em> &gt; m = </em> 0<em>，</em></p>
<p>Windows 2000： <em>x =</em> 0 <em>到</em> 3</p>
<p>Windows XP 及更高版本： <em>x =</em> 0 <em>或</em> 1</p></td>
<td><p><em>"LPT node.js</em>"，</p>
<p><em>n = m +</em>1</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284 链设备</p></td>
<td><p>PDO</p></td>
<td><p>无</p></td>
<td><p>"\Device\Parallel<em>m.</em></p>
<p><em>m</em> &gt; = 0</p></td>
<td><p>"LPT<em>n.</em>4"</p>
<p><em>n = m +</em>1</p></td>
</tr>
</tbody>
</table>

 

例如，以下设备名称和符号链接将分配给 " \\ device \\ ParallelPort0"，它具有两个 ieee 1284.3 菊花链设备和一个附加了 ieee 1284 终结链设备。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>设备类型</th>
<th>设备对象</th>
<th>内部名称</th>
<th>符号链接</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>并行端口</p></td>
<td><p>FDO</p></td>
<td><p>"\Device\ParallelPort0"</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284.3 设备</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.0"</p></td>
<td><p>"LPT 1.0"</p></td>
</tr>
<tr class="odd">
<td><p>IEEE 1284.3 设备</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.1"</p></td>
<td><p>"LPT 1.1"</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284 链设备</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.4"</p></td>
<td><p>"LPT 1.4"</p></td>
</tr>
</tbody>
</table>

 

 

 




