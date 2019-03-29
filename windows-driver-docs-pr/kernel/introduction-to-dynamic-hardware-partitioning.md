---
title: 动态硬件分区简介
description: 动态硬件分区简介
ms.assetid: 0d909c64-17c4-4f0e-85b7-4e0a6a92eeee
keywords:
- 动态硬件分区 WDK，有关动态硬件分区
- 硬件分区 WDK 动态的有关动态硬件分区
- 有关动态硬件分区，分区 WDK 动态硬件，
- 硬件可分区服务器 WDK
- 分区单位 WDK 动态硬件分区
- 以静态方式可分区服务器 WDK 动态硬件分区
- 动态可分区服务器 WDK 动态硬件分区
- 热添加 WDK 动态硬件分区
- 热删除 WDK 动态硬件分区
- 热替换 WDK 动态硬件分区
- 服务器 WDK 动态硬件分区
- 硬件分区 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b98066d47c7d25a8d14ec2dabf4648b15252c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576326"
---
# <a name="introduction-to-dynamic-hardware-partitioning"></a>动态硬件分区简介


一个*硬件可分区服务器*是可配置为一个或多个独立的服务器*硬件分区*。 每个硬件分区运行操作系统的独立实例。 可以将每个服务器的硬件资源分配给每个所适用于服务器的应用程序的任何配置中的各种硬件分区。 分配给特定的硬件分区的硬件资源彼此之间的服务器中的其他硬件分区。

硬件分区包含一个或多个*分区单位*。 分区单位是硬件的可以分配给硬件分区的最小单位。 分区单位可以是一个处理器、 内存模块或 I/O 主桥。 通常情况下，可以打开或关闭电源的套接字到插入处理器和内存模块独立。

硬件可分区服务器可以是两种类型之一：*静态可分区*或*可动态分区*。 在静态可分区服务器上，不能更改的服务器运行时分配给每个硬件分区的分区单元的配置。 若要更改的配置，必须关闭并重新启动服务器计算机。 Microsoft Windows Server 2000 和更高版本的 Windows Server 操作系统支持静态可分区服务器。

在动态可分区服务器上，您可以更改的服务器运行时分配给每个硬件分区的分区单位的配置。 这称为*动态硬件分区*。 如果硬件分区运行的操作系统支持动态硬件分区，您可以添加、 替换或删除无需重新启动操作系统分区单元。 具体取决于操作系统的功能，可以执行一个或多个以下的动态硬件分区操作：

<a href="" id="hot-add"></a>*热添加*  
将分区单元添加到正在运行的硬件分区。

<a href="" id="hot-remove"></a>*热删除*  
从正在运行的硬件分区中删除分区单元。

<a href="" id="hot-replace"></a>*热替换*  
分区单元替换为服务器计算机中已存在的相同替换分区单元。 热替换操作是单个操作不同于在热删除操作之后执行的一个热添加操作。

Windows Server 2003 Service Pack 1 (SP1) 支持热添加内存模块的操作在基于 x86 的、 基于 x64 和基于 Itanium 的服务器上。 Windows Server 2003 SP1 不支持热删除或热替换操作。

从 Windows Server 2008 开始，操作系统支持热添加处理器、 内存模块和 I/O 主桥的操作和热替换操作处理器和内存模块基于 x64 和基于 Itanium 的服务器计算机上。 操作系统也支持热添加内存模块的操作在基于 x86 的服务器计算机上。 操作系统不支持热删除操作。

下表总结了动态硬件分区支持，包括每个版本的 Windows Server 中。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Windows Server 2003 sp1</th>
<th>Windows Server 2008 和 Windows Server 的基于 x86 的服务器上的更高版本</th>
<th>Windows Server 2008 和更高版本的 Windows Server 的基于 x64 和基于 Itanium 的服务器上</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>热添加</p></td>
<td><p>内存模块</p></td>
<td><p>内存模块</p></td>
<td>处理器、 内存模块 I/O 承载桥</td>
</tr>
<tr class="even">
<td><p>热删除</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>热替换</p></td>
<td></td>
<td></td>
<td>处理器、 内存模块</td>
</tr>
</tbody>
</table>

 

我们建议开发设备驱动程序时请考虑以下准则：

-   您应该了解动态硬件分区因为了假设服务器计算机的硬件配置上动态可分区服务器无效。 设备驱动程序未设计为可以容纳动态硬件分区可能导致数据损坏或者要生成一个错误检查，如果动态可分区服务器上运行的操作系统。

-   应考虑[关键问题](critical-issues-for-device-drivers.md)标识用于动态硬件分区，即使你不开发服务器的计算机的设备驱动程序。

-   您应查看并更新为运行 Windows Server 2008 和更高版本的 Windows Server 的服务器正在开发的所有设备驱动程序。 设备驱动程序可以使用操作系统的硬件配置的更改通知注册。 在得到有关硬件配置的更改的通知的设备驱动程序，它们可以响应所需的安全和最佳操作的更改。 这可确保动态可分区服务器上正确的驱动程序函数。

您开发适用于 Windows XP 和更高版本的正确参与的 Windows 的驱动程序[资源重新平衡](stopping-a-device-to-rebalance-resources.md)，而不进行任何假设处理器、 处理器关联掩码或量的数目物理内存中，将继续正常运行的动态可分区服务器上。

大多数现有的用户模式应用程序应继续在无需任何修改动态可分区服务器上运行。 但是，如果应用程序分配的每个处理器的线程或执行基于物理内存量是可用的内存分配时，可以向操作系统的硬件配置的更改通知注册应用程序。 当有关硬件配置的更改通知应用程序时，它可以相应地调整其资源分配。

 

 




