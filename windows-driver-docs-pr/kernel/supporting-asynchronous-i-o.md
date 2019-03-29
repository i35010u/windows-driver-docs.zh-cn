---
title: 支持异步 I/O
description: 支持异步 I/O
ms.assetid: b4baf1a9-6156-4bbf-b4d9-7205924c637f
keywords:
- 异步 I/O WDK 内核
- I/O WDK 内核，异步模式
- WDK I/O 请求的状态信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0087723df0b61e2ee506d69325a44bbd530069f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568382"
---
# <a name="supporting-asynchronous-io"></a>支持异步 I/O





I/O 管理器提供支持异步 I/O，使 （通常在用户模式应用程序，但有时其他驱动程序） 的 I/O 请求的发起方可以继续执行，而不是等待其 I/O 请求完成。 异步 I/O 支持提高了整体系统的吞吐量和发出的 I/O 请求的任何代码的性能。

利用异步 I/O 支持，内核模式驱动程序不一定处理 I/O 请求发送到 I/O 管理器的顺序相同。 I/O 管理器或更高级别的驱动程序，可以重新排序 I/O 请求，因为它们被接收。 驱动程序可以拆分为较小的传输请求的大型数据传输请求。 此外，驱动程序可以重叠 I/O 请求处理，尤其是在对称多处理器平台，如中所述[包含多个处理器安全](multiprocessor-safe.md)。

此外，内核模式驱动程序处理单个 I/O 请求是不一定是序列化。 也就是说，驱动程序不一定处理完成每个 IRP 开始处理下一个传入的 I/O 请求之前。

当驱动程序接收 IRP 时，它响应通过尽可能特定于 IRP 的处理，因为它可以执行。 如果该驱动程序支持异步 IRP 处理，它可以将 IRP 发送到下一步的驱动程序，如有必要，并开始处理下一步 IRP，而无需等待完成的第一个。 该驱动程序可以注册"完成例程，"I/O 管理器调用时另一个驱动程序已完成处理 IRP。 驱动程序状态中提供值 IRP 的 I/O 状态块，可以访问其他驱动程序来确定的 I/O 请求的状态。

驱动程序可以维护其当前的 I/O 操作在其设备对象，调用的特殊部分中的状态信息[设备扩展](device-extensions.md)。

有关详细信息，请参阅[处理 Irp](handling-irps.md)并[输入/输出技术](i-o-programming-techniques.md)。

 

 




