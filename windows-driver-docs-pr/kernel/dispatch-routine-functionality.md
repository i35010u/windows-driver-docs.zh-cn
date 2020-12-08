---
title: Dispatch 例程的功能
description: Dispatch 例程的功能
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 30b6a7492f068e016f4c81a8ab1784e2da43e758
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799477"
---
# <a name="dispatch-routine-functionality"></a>Dispatch 例程的功能





特定调度例程所需的功能根据其处理的 i/o 函数代码、单个驱动程序在驱动程序链中的位置以及基础物理设备的类型而有所不同。

大多数调度例程处理 (Irp) 传入的 i/o 请求包，如下所示：

1. 检查 IRP 中驱动程序的 i/o 堆栈位置，以确定要执行的操作并检查参数（如果有）的有效性。

   驱动程序是否必须检查其 i/o 堆栈位置以确定要执行的操作以及检查参数取决于给定的 **irp \_ mj \_**<em>xxx</em>，以及该驱动程序是否为驱动程序处理的每个 **IRP \_ \_ mj**<em>xxx</em>设置单独的调度例程。

2. 满足请求并完成 IRP （如果可能）;否则，将其传递给更低级别的驱动程序或其他设备驱动程序例程进行进一步处理。

   驱动程序是否必须通过 irp 进行进一步处理取决于参数的有效性（如果有），以及在层次驱动程序链中的 **IRP \_ MJ \_**<em>XXX</em>和驱动程序级别（如果有）。

有关 Irp 的详细信息，请参阅 [处理 irp](handling-irps.md)。

 

 




