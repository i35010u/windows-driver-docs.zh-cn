---
title: Storport 的接口与 Storport 微型端口驱动程序
description: Storport 的接口与 Storport 微型端口驱动程序
ms.assetid: 8e09d6a6-7e4f-44fc-a2b0-5f21b4ac0593
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90c43df04cdedd9d8f93d53aad2969b94abe8607
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325711"
---
# <a name="storports-interface-with-storport-miniport-drivers"></a>Storport 的接口与 Storport 微型端口驱动程序


之间的通信 Storport 驱动程序和 Storport 微型端口驱动程序都通过 SCSI 请求块 (Srb) 和微型端口驱动程序回调例程。 Storport 微型端口驱动程序回调例程的详细讨论，请参阅[Storport 驱动程序微型端口例程](https://msdn.microsoft.com/library/windows/hardware/ff567543)。

有关概述，以及各个 SRB 函数、 SRB 标志和 SRB 状态值的定义，请参阅[ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393)。

有关如何微型端口驱动程序必须应对每个 SRB 函数的讨论，请参阅[ **HwStorStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557423)。

Storport 将 Srb 转发到 Storport 微型端口驱动程序以进行异步处理。 通常情况下，微型端口驱动程序将需要一些时间来实际完成该请求。 支持有标记的队列的主机总线适配器可以在内部对请求进行排队，并指示由标记 Storport 分配到每个请求的顺序处理它们。 [ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393) (SRB) 结构包含两个成员 Storport 驱动程序用来指定 Srb 主机适配器的内部队列中的排序方式:**QueuedTag**并**QueueAction**。 Storport 分配计数，或 *"标记"* 值，为**QueuedTag**指示适配器应在其中处理的数据包的顺序的每个 SRB 的成员。 标记值还允许 Storport 跟踪哪些 Srb 已成功完成，哪些 Srb 已超时。

**QueueAction**成员分配以下值之一：

SRB\_简单\_标记\_请求

SRB\_HEAD\_OF\_队列\_标记\_请求

SRB\_ORDERED\_队列\_标记\_请求

有关这些值的说明，请参阅 scsi-3 规范。

 

 




