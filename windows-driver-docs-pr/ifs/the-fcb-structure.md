---
title: FCB 结构
description: FCB 结构
ms.assetid: feb38b24-c028-4c8d-be45-11d9a4659f8d
keywords:
- 文件控制块结构 WDK RDBSS
- FCB WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3680969457f0a74aecf5a0c35fbad29858043361
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577256"
---
# <a name="the-fcb-structure"></a>FCB 结构


## <span id="ddk_the_fcb_structure_if"></span><span id="DDK_THE_FCB_STRUCTURE_IF"></span>


指向文件控制块 (FCB) 结构*FsContext*字段中的文件对象。 共享 FCB 的操作的所有引用同一个文件。 遗憾的是，SMB 服务器是目前的实现方式的名称可以是一个别名，以便两个不同的名称可能是相同的文件。 FCB 是文件操作的焦点。 由于对相同 FCB 的操作实际上是在同一文件中的同步基于 FCB 而不是某些更高级别对象。

每当创建 FCB 结构，相应 SRV\_打开和 FOBX 结构还会创建。 多个 SRV\_打开结构可以是与给定的 FCB 结构，关联，并且多个 FOBX 结构给定 SRV 与相关联\_打开结构。 在大多数情况下，一个 SRV\_打开结构与 FCB 相关联，并且给定 SRV 与关联的 FOBX 结构数\_打开结构为 1。 若要提高空间局部性和分页行为在这种情况下，为 FCB 结构分配也会涉及分配一个关联 SRV\_打开和 FOBX 结构。

尝试分配关联的 FCB，SRV RDBSS\_打开，和 FOBX 结构中的内存来提高分页行为合并在一起。 RDBSS 不会分配 FCB 和 NET\_根结构一起因为 NET\_不分页根结构，但 FCB 结构通常都分页 （除非它们是分页文件）。

FCB 结构对应于每个打开的文件和目录。 FCB 结构拆分为以下两个部分：

-   非分页的一部分中非分页缓冲池分配

-   分页的一部分

前者是非\_PAGED\_FCB 及更高版本称为 FCB。

FCB 包含指向相应的非\_PAGED\_FCB 一部分。 从非维护的反向指针\_PAGED\_出于调试目的在 FCB 的 FCB 检查版本。

非\_PAGED\_FCB 包含的内存管理器和缓存管理器用来操作部分的对象的特殊指针的结构。 请注意，这些指针的值通常设置在文件系统之外。

FCB 结构包含以下元素：

-   FSRTL\_常见\_标头结构

-   签名和引用计数

-   名称和关联的表信息

-   向相关联的.NET 的反向指针\_根结构

-   一组相关联的 SRV\_打开结构

-   设备对象

-   根据网络微型重定向或 FCB 结构的创建者的请求任何其他存储

 

 




