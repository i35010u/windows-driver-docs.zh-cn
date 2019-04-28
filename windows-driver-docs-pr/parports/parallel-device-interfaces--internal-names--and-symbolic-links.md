---
title: 并行设备接口、内部名称和符号链接
description: 并行设备接口、内部名称和符号链接
ms.assetid: 859e20bb-e411-4572-a393-a6faf534cf15
keywords:
- 系统提供并行驱动程序 WDK，设备接口
- 系统提供并行驱动程序 WDK，内部名称
- 系统提供并行驱动程序 WDK，符号链接
- 设备接口 WDK 并行驱动程序
- WDK 并行驱动程序的符号链接
- WDK 并行驱动程序的内部名称
- WDK 并行驱动程序名称
- 未受保护的符号链接 WDK
- 并行设备 WDK，设备接口
- 设备对象 WDK 并行驱动程序
- 并行设备 WDK，内部名称
- 并行设备 WDK，符号链接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9c42d60a12a90939048987b3b75d78058b71586
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351951"
---
# <a name="parallel-device-interfaces-internal-names-and-symbolic-links"></a>并行设备接口、内部名称和符号链接





本部分介绍设备接口、 内部名称，并由系统提供并行和驱动程序的并行端口连接到的并行端口的设备创建的符号链接。

有关枚举系统中的每个并行端口和并行端口上枚举每个并行设备，并行驱动程序创建设备对象、 接口、 内部名称和未受保护的符号链接，如下所示。

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
<td><p>"\Device\ParallelPort<em>m",</em></p>
<p><em>m &gt;=</em> 0</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>原始并行设备</p></td>
<td><p>PDO</p></td>
<td><p>GUID_PARCLASS_DEVICE</p></td>
<td><p>"\Device\Parallel<em>m</em>",</p>
<p><em>m &gt;=</em> 0</p></td>
<td><p>"LPT<em>n</em>",</p>
<p><em>n = m +</em> 1</p></td>
</tr>
<tr class="odd">
<td><p>IEEE 1284.3 设备</p></td>
<td><p>PDO</p></td>
<td><p>无</p></td>
<td><p>"\Device\Parallel<em>m.x</em>",</p>
<p><em>m &gt;=</em> 0<em>,</em></p>
<p>Windows 2000: <em>x =</em> 0<em>到</em>3</p>
<p>Windows XP 及更高版本： <em>x =</em> 0<em>或</em>1</p></td>
<td><p>"LPT<em>n.x</em>",</p>
<p><em>n = m +</em>1</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284 链结束设备</p></td>
<td><p>PDO</p></td>
<td><p>无</p></td>
<td><p>"\Device\Parallel<em>m.</em>4"</p>
<p><em>m</em> &gt;= 0</p></td>
<td><p>"LPT<em>n.</em>4"</p>
<p><em>n = m +</em>1</p></td>
</tr>
</tbody>
</table>

 

例如，以下的设备名称和符号链接分配给"\\设备\\ParallelPort0"，其中包含两个 IEEE 1284.3 菊花链设备和 IEEE 1284 链结束设备附加到它。

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
<td><p>"LPT1.0"</p></td>
</tr>
<tr class="odd">
<td><p>IEEE 1284.3 设备</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.1"</p></td>
<td><p>"LPT1.1"</p></td>
</tr>
<tr class="even">
<td><p>IEEE 1284 链结束设备</p></td>
<td><p>PDO</p></td>
<td><p>"\Device\Parallel0.4"</p></td>
<td><p>"LPT1.4"</p></td>
</tr>
</tbody>
</table>

 

 

 




