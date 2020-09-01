---
title: 将整个驱动程序分页
description: 将整个驱动程序分页
ms.assetid: d861160f-e429-4ff3-9ca6-4fce4d5d6c1b
keywords:
- 可分页驱动程序 WDK 内核，分页整个驱动程序
- 分页整个驱动程序 WDK
- 引用计数 WDK 可分页驱动程序
- 重写可分页或不可分页属性 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56cf610d4b57c4ca1b8a4b7a36531c66c9c36a7b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191851"
---
# <a name="paging-an-entire-driver"></a>将整个驱动程序分页





使用 **MmLockPagable * Xxx*** 支持例程并指定分页和可放弃部分的驱动程序由未分页的部分、分页部分和初始化驱动程序后放弃的 INIT 部分组成。

设备驱动程序连接它管理的设备的中断后，驱动程序的中断处理路径必须在系统空间中。 中断处理代码必须是无法分页的驱动程序部分的一部分，以防发生中断。

另外两个内存管理器例程（ [**MmPageEntireDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmpageentiredriver) 和 [**MmResetDriverPaging**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmresetdriverpaging)）可用于替代构成驱动程序映像的所有部分的可分页或不可分页属性。 当驱动程序所管理的设备未被使用并且无法生成中断时，这些例程可以使驱动程序完全分页。

完全可分页的系统驱动程序的示例包括 win32k.sys 驱动程序、串行驱动程序、mailslot 驱动程序、蜂鸣驱动程序和 null 驱动程序。

串行驱动程序通常会间歇地使用。 在打开它管理的端口之前，串行驱动程序可以完全分页。 打开端口后，必须将内存驻留的串行驱动程序的部分置于非分页系统空间。 驱动程序的其他部分可以保持可分页。

在连接中断之前，可以完全分页的驱动程序应在驱动程序初始化期间调用 **MmPageEntireDriver** 。

当由分页的驱动程序管理的设备收到打开的请求时，驱动程序将在中分页。 然后，驱动程序必须在连接到中断之前调用 [**MmResetDriverPaging**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmresetdriverpaging) 。 调用 **MmResetDriverPaging** 会使内存管理器根据在编译和链接过程中获取的属性来处理驱动程序的部分。 未分页的任何部分（例如文本部分）都将分页到未分页的系统内存中;可分页节将在被引用时分页。

此类驱动程序必须在其设备上保留打开句柄的引用计数。 该驱动程序将递增每个打开请求的计数，并在每个关闭请求时减少计数。 当计数达到零时，驱动程序应断开中断，然后调用 **MmPageEntireDriver**。 如果驱动程序管理多个设备，则所有此类设备的计数必须为零，驱动程序才能调用 **MmPageEntireDriver**。

驱动程序的责任是在更改引用计数时执行任何需要的同步，并在驱动程序的可分页状态发生变化时阻止引用计数更改。 也就是说，在 SMP 计算机中，驱动程序必须确保 **MmPageEntireDriver** 在一个处理器上无法进行，而在另一个处理器上，打开的调用会导致连接中断，并且引用计数将递增。

 

