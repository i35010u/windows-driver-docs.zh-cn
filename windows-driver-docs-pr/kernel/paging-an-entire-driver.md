---
title: 将整个驱动程序分页
description: 将整个驱动程序分页
ms.assetid: d861160f-e429-4ff3-9ca6-4fce4d5d6c1b
keywords:
- 可分页的驱动程序 WDK 内核，分页整个驱动程序
- 分页整个驱动程序 WDK
- 引用计数 WDK 可分页的驱动程序
- 重写可分页或 nonpageable 特性 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 077c8971e68ad710c47438f5b4ad9338c8e4f433
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567985"
---
# <a name="paging-an-entire-driver"></a>将整个驱动程序分页





使用的驱动程序**MmLockPagable * Xxx*** 支持例程，并指定分页和可放弃部分包含非分页的部分、 分页的部分中和驱动程序初始化之后，将放弃 INIT 部分。

设备驱动程序连接中断它所管理的设备后，驱动程序的中断处理路径必须驻留在系统空间中。 在发生中断时的情况下，中断处理代码必须是不能换出，驱动程序部分的一部分。

两个额外的内存管理器例程[ **MmPageEntireDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff554650)并[ **MmResetDriverPaging**](https://msdn.microsoft.com/library/windows/hardware/ff554680)，可用于重写可分页或 nonpageable 属性组成的驱动程序映像的所有部分。 这些例程启用分页出整个时它所管理的设备未被使用，无法生成中断的驱动程序。

完全可分页的系统驱动程序的示例包括 win32k.sys 驱动程序、 串行驱动程序、 邮件槽驱动程序、 提示音驱动程序和 null 的驱动程序。

串行驱动程序通常会间歇性地使用。 只有先打开它所管理的端口，串行驱动程序可以出页完全。 一旦打开某个端口时，必须驻留在内存中的串行驱动程序的各个部分必须置于非分页的系统空间。 该驱动程序的其他部分可以保持可分页。

可以完全调出的驱动程序应调用**MmPageEntireDriver**驱动程序初始化之前中断连接过程。

当调出驱动程序管理的设备收到了打开请求时，该驱动程序中分页。 然后，该驱动程序必须调用[ **MmResetDriverPaging** ](https://msdn.microsoft.com/library/windows/hardware/ff554680)它连接到中断之前。 调用**MmResetDriverPaging**导致内存管理器将驱动程序的部分根据在编译和链接过程中获取的属性。 为非分页，如文本部分中，任何部分将分页到非分页的系统内存;被引用，将在分页可分页的部分。

此类驱动程序必须向其设备保持打开的句柄的引用计数。 该驱动程序增加在任何设备和减少每次打开请求的计数在每个关闭的请求计数。 该驱动程序时计数达到零时，应断开连接中断，然后调用**MmPageEntireDriver**。 如果驱动程序管理多台设备，计数必须先为零的所有此类设备驱动程序可以调用**MmPageEntireDriver**。

在驱动程序负责执行任何同步时是必需的更改的引用计数，并以避免引用计数更改时，驱动程序的可分页状态已更改。 即，在 SMP 计算机，该驱动程序必须确保**MmPageEntireDriver**正在一个处理器，在另一个处理器上，对 open 的调用会引起中断连接和引用计数为不能为递增。

 

 




