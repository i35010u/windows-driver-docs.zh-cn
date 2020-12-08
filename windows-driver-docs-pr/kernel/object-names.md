---
title: 对象名称
description: 对象名称
keywords:
- 对象名称 WDK 内核
- 命名对象 WDK 内核
- 未命名对象 WDK 内核
- 对象名称 WDK 用户模式
- 对象处理 WDK 用户模式
- 对象处理 WDK 内核
- 处理 WDK 用户模式
- 处理 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e31b36d69fd9f78c13da221045eca5f47703e4af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837711"
---
# <a name="object-names"></a>对象名称





内核模式对象已命名或未命名。 *对象名称* 是一个 Unicode 字符串，用户模式和内核模式组件都可以使用它来引用对象。 例如， **\\ KernelObjects \\ LowMemoryCondition** 是标准事件对象的名称，该对象在系统中的可用内存量较低时发出信号。

用户模式和内核模式组件都使用对象名称打开对象的句柄。 所有后续操作都通过使用句柄来执行。

如果对象未命名，用户模式组件将无法打开该对象的句柄。 内核模式组件可以通过指针或句柄来引用未命名对象。

命名对象组织为一个层次结构。 每个对象都是相对于父对象的名称。 对象名称的每个组件都以反斜杠字符开头。 例如， **\\ KernelObjects** 是 **\\ KernelObjects \\ LowMemoryCondition** 的父对象。

只有某些类型的对象可以有子对象。 下面是一些示例：

-   对象目录具有子对象。 对象管理器使用对象目录来组织对象。 例如， **\\ KernelObjects** 是包含标准事件对象的对象目录。 对象目录不与磁盘上的实际目录相对应。 有关详细信息，请参阅 [对象目录](object-directories.md)。

-   磁盘驱动器的设备对象具有与磁盘上的文件相对应的子对象。

-   表示目录的文件对象具有与目录中的文件相对应的子对象。

-   WDM 驱动程序的设备对象具有自己的命名空间，可在驱动程序定义的方式中使用。 有关详细信息，请参阅 [控制设备命名空间访问](controlling-device-namespace-access.md)。

文件具有相对于 **\\ DosDevices** 的对象名称。 例如，可以将 file c： \\ directory \\ 文件指定为 **\\ DosDevices \\ C \\ ：**<em>directory \\ 文件</em>。

例如，可以按如下所述描述对象名称的组件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>对象名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>\DosDevices</strong></p></td>
<td><p>对象目录。</p></td>
</tr>
<tr class="even">
<td><p><strong>\DosDevices\C:</strong></p></td>
<td><p>表示 C：驱动器的设备对象。</p></td>
</tr>
<tr class="odd">
<td><p><strong>\DosDevices\C： \</strong><em>目录</em></p></td>
<td><p>表示名为 C:\Directory. 的目录的文件对象</p></td>
</tr>
<tr class="even">
 <td><p><strong>\DosDevices\C： \</strong><em>目录</em> \ <em>文件</em></p></td>
<td><p>表示名为 C:\Directory\File. 的文件的文件对象</p></td>
</tr>
</tbody>
</table>

 

创建命名对象的驱动程序在特定对象目录中执行此操作。 有关详细信息，请参阅 [对象目录](object-directories.md)。

 

 




