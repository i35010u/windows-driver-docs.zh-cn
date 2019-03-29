---
title: Dispatch 例程的功能
description: Dispatch 例程的功能
ms.assetid: cfc191af-2b65-465b-972e-9617a8f7d8b7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 762601118e8db795691aabb7407796c0c498b690
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562003"
---
# <a name="dispatch-routine-functionality"></a>Dispatch 例程的功能





在特定的调度例程所需的功能各不相同，具体取决于它处理，在单独的驱动程序的驱动程序，链中的位置和基础物理设备的类型上的 I/O 函数代码。

大多数的调度例程处理传入的 I/O 请求数据包 (Irp)，如下所示：

1. 检查在 IRP，以确定要做，如果有的有效性检查参数，驱动程序的 I/O 堆栈位置。

   驱动程序是否必须检查其 I/O 堆栈位置，以便确定程序执行并检查参数的内容取决于给定**IRP\_MJ\_**<em>XXX</em>，以及在无论该驱动程序设置注册每个单独的调度例程**IRP\_MJ\_**<em>XXX</em>驱动程序处理。

2. 满足请求，并在可能的情况; 完成 IRP否则，将它传递进行进一步处理的较低级驱动程序或由其他设备驱动程序例程。

   如果有的话，以及是否驱动程序必须传递 IRP 进行进一步处理依赖于参数的有效性**IRP\_MJ\_**<em>XXX</em>和驱动程序的级别，如果任何，链中的分层驱动程序。

有关 Irp 的详细信息，请参阅[处理 Irp](handling-irps.md)。

 

 




