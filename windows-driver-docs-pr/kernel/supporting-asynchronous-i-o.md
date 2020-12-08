---
title: 支持异步 I/O
description: 支持异步 I/O
keywords:
- 异步 i/o WDK 内核
- I/o WDK 内核，异步模式
- 状态信息 WDK i/o 请求数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba925b10d116078e011574b79cb40eaa1c593c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827643"
---
# <a name="supporting-asynchronous-io"></a>支持异步 I/O





I/o 管理器提供异步 i/o 支持，以便 i/o 请求的发起方 (通常是用户模式的应用程序，但有时其他驱动程序) 可以继续执行，而不是等待其 i/o 请求完成。 异步 i/o 支持改善了整体系统吞吐量和发出 i/o 请求的任何代码的性能。

利用异步 i/o 支持，内核模式驱动程序不一定按将 i/o 请求发送到 i/o 管理器的相同顺序处理这些请求。 I/o 管理器或更高级别的驱动程序可以在收到 i/o 请求时对其重新排序。 驱动程序可以将大型数据传输请求拆分为较小的传输请求。 而且，驱动程序可以重叠 i/o 请求处理，尤其是在对称多处理器平台中，如 [多处理器安全](multiprocessor-safe.md)中所述。

而且，不一定要对内核模式驱动程序处理单个 i/o 请求进行序列化。 也就是说，驱动程序在开始处理下一个传入 i/o 请求之前，不一定会处理每个 IRP 完成。

当驱动程序收到 IRP 时，它会通过尽可能多地执行 IRP 特定的处理来做出响应。 如果驱动程序支持异步 IRP 处理，则它可以将 IRP 发送到下一个驱动程序（如有必要），并开始处理下一个 IRP，而不必等待第一个 IRP 完成。 该驱动程序可以注册一个 "完成例程"，当另一个驱动程序完成了 IRP 的处理时，i/o 管理器会调用它。 驱动程序在 IRP 的 i/o 状态块中提供状态值，其他驱动程序可以访问这些值来确定 i/o 请求的状态。

驱动程序可以在其设备对象（称为 [设备扩展](device-extensions.md)）的特殊部分中维护有关其当前 i/o 操作的状态信息。

有关详细信息，请参阅 [处理 irp](handling-irps.md) 和 [输入/输出技术](i-o-programming-techniques.md)。

 

 




