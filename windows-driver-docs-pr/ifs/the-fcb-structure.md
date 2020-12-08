---
title: FCB 结构
description: FCB 结构
keywords:
- 文件控制块结构 WDK RDBSS
- FCB WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87311346a3461df13e74d2669207640d3dd4d873
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813213"
---
# <a name="the-fcb-structure"></a>FCB 结构


## <span id="ddk_the_fcb_structure_if"></span><span id="DDK_THE_FCB_STRUCTURE_IF"></span>


文件对象中的 *FsContext* 字段指向 (FCB) 结构的文件控制块。 共享 FCB 的所有操作都引用同一个文件。 遗憾的是，SMB 服务器现在的实现方式可以是别名，因此，两个不同的名称可以是同一文件。 FCB 是文件操作的焦点。 由于对相同 FCB 的操作实际上位于同一个文件中，因此，同步基于 FCB 而不是一个更高级别的对象。

只要创建 FCB 结构， \_ 也会创建相应的 SRV 开放和 FOBX 结构。 可以将多个 SRV \_ 开放式结构与给定的 FCB 结构相关联，并且多个 FOBX 结构与给定的 SRV \_ 开放结构关联。 在大多数情况下，一个 SRV \_ 开放式结构与一个 FCB 关联，而与给定 SRV 开放式结构关联的 FOBX 结构的数目 \_ 为1。 为了改进此类情况下的空间区域和分页行为，FCB 结构的分配还涉及到一个关联的 SRV \_ OPEN 和 FOBX 结构的分配。

RDBSS 尝试将关联的 FCB、SRV \_ 打开和 FOBX 结构一起分配到内存中，以提高分页行为。 RDBSS 不会将 FCB 和 NET \_ 根结构一起分配到一起，因为网络 \_ 根结构未分页，但 FCB 结构通常 (分页，除非它们) 的页面文件。

FCB 结构对应于每个打开的文件和目录。 FCB 结构分为以下两部分：

-   在非分页池中分配的非分页部件

-   页面式部件

前者是非 \_ 分页 \_ FCB，后面称为 FCB。

FCB 包含指向对应的非 \_ 分页 \_ FCB 部分的指针。 在已检查的生成中，反向指针将从非 \_ 分页 FCB 维护为 \_ FCB，以便进行调试。

非 \_ 分页 \_ FCB 包含内存管理器和缓存管理器用来处理节对象的特殊指针的结构。 请注意，这些指针的值通常在文件系统外设置。

FCB 结构包含以下内容：

-   FSRTL \_ 通用 \_ 标头结构

-   签名和引用计数

-   名称和关联的表信息

-   反向指针到关联的网络 \_ 根结构

-   关联的 SRV \_ 开放式结构列表

-   Device 对象

-   网络小型重定向程序或 FCB 结构创建者请求的任何其他存储

 

 




