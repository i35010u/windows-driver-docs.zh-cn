---
title: 对象名称
description: 对象名称
ms.assetid: b30e7475-7f94-4993-b373-8e4a8b1bcb4c
keywords:
- 对象名称 WDK 内核
- 命名的对象 WDK 内核
- 未命名的对象 WDK 内核
- 对象名称 WDK 用户模式
- 对象将处理 WDK 用户模式
- 对象句柄 WDK 内核
- 句柄 WDK 用户模式
- 句柄 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd7fdf24eb420f670fe5234fc8e5a17d985ff7af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543928"
---
# <a name="object-names"></a>对象名称





内核模式的对象名为连接，或者未命名的。 *对象名称*是用户模式和内核模式组件可用于引用对象的 Unicode 字符串。 例如，  **\\KernelObjects\\LowMemoryCondition**是向系统中的可用内存量较低时发出信号的标准事件对象的名称。

用户模式和内核模式组件使用的对象名称以打开对象的句柄。 通过使用句柄进行所有后续操作。

如果未命名对象，用户模式组件无法打开的句柄。 内核模式组件可以引用一个未命名对象的指针或句柄。

命名的对象被组织到层次结构。 每个对象被命名为相对于父对象。 反斜杠字符开头的对象名称的每个组件。 例如，  **\\KernelObjects**是父对象 **\\KernelObjects\\LowMemoryCondition**。

仅某些类型的对象可以包含子对象。 以下是一些示例：

-   对象目录包含子对象。 对象管理器使用对象目录来组织对象。 例如 **\\KernelObjects**是保存标准事件对象的对象目录。 对象目录不对应于磁盘上的实际目录。 有关详细信息，请参阅[对象目录](object-directories.md)。

-   磁盘驱动器的设备对象具有与磁盘上的文件相对应的子对象。

-   表示目录的文件对象具有子对象对应于目录中的文件。

-   用于 WDM 驱动程序的设备对象具有自己可以以驱动程序定义的方式使用的命名空间。 有关详细信息，请参阅[控制设备 Namespace 访问](controlling-device-namespace-access.md)。

文件具有相对于的对象名称 **\\DosDevices**。 例如，文件 c:\\Directory\\文件可以指定为 **\\DosDevices\\c:\\**<em>目录\\文件</em>.

例如，可以按如下所示描述的对象名称的组件。

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
<td><p>表示 c： 驱动器的设备对象。</p></td>
</tr>
<tr class="odd">
<td><p><strong>\DosDevices\C:&lt;/strong&gt; <em>Directory</em></p></td>
<td><p>文件对象，表示名为 C:\Directory 的目录。</p></td>
</tr>
<tr class="even">
<td><p><strong>\DosDevices\C:&lt;/strong&gt; <em>Directory</em> \ <em>File</em></p></td>
<td><p>文件对象，表示名为 C:\Directory\File 的文件。</p></td>
</tr>
</tbody>
</table>

 

驱动程序创建的对象名为此，在特定对象的目录中。 有关详细信息，请参阅[对象目录](object-directories.md)。

 

 




