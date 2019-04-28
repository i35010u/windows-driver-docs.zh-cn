---
title: 连接和文件结构管理
description: 连接和文件结构管理
ms.assetid: 3695cab3-6751-48ee-8b11-e70c2bceab29
keywords:
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26e1683aee9da29d2514b8c193983bdf92fa0d94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351420"
---
# <a name="connection-and-file-structure-management"></a>连接和文件结构管理


## <span id="ddk_connection_and_file_structure_management_if"></span><span id="DDK_CONNECTION_AND_FILE_STRUCTURE_MANAGEMENT_IF"></span>


有六个 RDBSS 用于管理连接和文件结构的基本数据结构。 通过 RDBSS 和各种网络的最小重定向，将在内部使用这些数据结构。 有两个版本的这些数据结构。 网络微型重定向版本包含可以由网络微型重定向程序驱动程序操作的字段。 这些数据结构的网络微型重定向版本开头 MRX\_前缀。 RDBSS 版本包含仅可以由 RDBSS 操作的其他字段。

这些六种基本数据结构如下所示：

-   SRV\_调用-服务器调用上下文。 此结构可提供远程服务器的抽象。

-   NET\_根-net 根。 此结构抽象化到一个共享的连接。

-   V\_NET\_根-net 根 （也称为虚拟 netroots） 的视图。

-   FCB-文件控制块。 此结构表示打开的文件共享上。

-   SRV\_打开-服务器端打开上下文。 此结构封装在服务器上的打开句柄。

-   FOBX-文件对象扩展名。 此结构是对 RDBSS 扩展[**文件\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff545834)结构。

以下层次结构中组织这些数据结构：

```cpp
                SRV_CALL 
     FCB   <------> NET_ROOT
        SRV_OPEN  <---> V_NET_ROOT
            FOBX
                FILE_OBJECT
```

内核的文件系统调用的响应，RDBSS 通常情况下创建的临近以及网络微型重定向程序驱动程序的前面提到的结构除 FOBX 结构。 因此，需要一些用于连接和文件结构管理的 RDBSS 例程的网络微型重定向程序驱动程序将正常情况下只能调用。 RDBSS 在内部调用这些例程的大多数。

所有这些数据结构都是引用计数。 上一种数据结构的引用计数是按如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">数据结构</th>
<th align="left">说明的引用计数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SRV_CALL</p></td>
<td align="left"><p>指向 SRV_CALL，再加上一些动态值的 NET_ROOT 条目数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NET_ROOT</p></td>
<td align="left"><p>FCB 条目和 V_NET_ROOT 项指向 NET_ROOT，再加上一些动态值的数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>V_NET_ROOT</p></td>
<td align="left"><p>指向 V_NET_ROOT，再加上一些动态值的 SRV_OPEN 条目数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FCB</p></td>
<td align="left"><p>指向 FCB，再加上一些动态值的 SRV_OPEN 条目数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SRV_OPEN</p></td>
<td align="left"><p>指向 SRV_OPEN，再加上一些动态值的 FOBX 条目数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FOBX</p></td>
<td align="left"><p>某些动态值。</p></td>
</tr>
</tbody>
</table>

 

在每种情况下，动态值是指已引用结构，而无需取消引用它的调用方的数目。 由这些例程本身进行维护的引用计数的静态部分。 例如， [ **RxCreateNetRoot** ](https://msdn.microsoft.com/library/windows/hardware/ff554366)递增关联 SRV 的引用计数\_调用结构。

引用调用和查找成功递增引用计数中;取消调用递减引用计数。 创建的例程调用分配一个结构，并将引用计数设置为 1。

与任何数据结构相关联的引用计数是至少为 1 加上的下一个较低级别与之关联的数据结构的实例。 例如，引用计数与 SRV\_调用，其中包含两个 NET\_与其关联的根是至少为 3。 除了由内部 RDBSS 引用**NameTable**结构和数据结构在下一级别降低，有可能获得的其他参考。

这些限制可确保在任何给定级别的数据结构不能被终结 （发布和释放相关联的内存块） 直到在下一个级别的数据结构的所有已完成，否则发布了它们的引用。 例如，如果对 FCB 的引用被保留，则可以安全地访问 V\_NET\_根，NET\_根和 SRV\_调用结构与之关联。

在网络重定向 mini 和 RDBSS 之间的接口中使用两个重要抽象是 SRV\_调用和 NET\_根结构。 SRV\_调用结构对应于与之建立连接，在服务器与关联的上下文和 NET\_根结构对应于 （这可能也会被视为命名空间的一部分的服务器上的共享这已被占用网络微型重定向）。

创建 SRV\_调用和 NET\_根结构通常包括至少一个网络往返。 若要提供有关异步操作以继续，这些操作被建模为两阶段的活动。 每个调用向下到网络微型-重定向器用于创建 SRV\_调用和 NET\_根结构都伴随 call-up 从网络微型重定向到 RDBSS 通知请求的完成状态。 当前这些是同步的。

创建 SRV\_调用结构得更加复杂，RDBSS 必须选择从多个网络微型-重定向程序建立与服务器的连接这一事实。 为提供最灵活地选择网络微型重定向其想要部署，请创建 SRV RDBSS\_结构涉及到在其中 RDBSS 通知网络微型重定向的入选方的第三个阶段的调用。 所有落选网络的最小重定向销毁相关联的上下文。

本部分包含以下主题：

[SRV\_调用结构](the-srv-call-structure.md)

[NET\_根结构](the-net-root-structure.md)

[V\_NET\_根结构](the-v-net-root-structure.md)

[FCB 结构](the-fcb-structure.md)

[SRV\_打开结构](the-srv-open-structure.md)

[FOBX 结构](the-fobx-structure.md)

[连接和文件结构锁定](connections-and-file-structure-locking.md)

[连接和文件控制块管理例程](connection-and-file-control-block-management-routines.md)

 

 




