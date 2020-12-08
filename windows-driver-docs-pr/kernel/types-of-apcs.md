---
title: APC 的类型
description: APC 的类型
keywords:
- 异步过程调用 WDK 内核
- Apc WDK 内核
- 用户 Apc WDK 内核
- 普通内核 Apc WDK 内核
- 特殊内核 Apc WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9944835441625c31670c585a07504f679e56d44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828535"
---
# <a name="types-of-apcs"></a>APC 的类型


APC)  (的异步过程调用是异步执行的函数。 Apc 类似于延迟过程调用 (Dpc) ，但与 Dpc 不同，Apc 在特定线程的上下文中执行。 除了文件系统和文件系统筛选器驱动程序以外，驱动程序 () 不会直接使用 Apc，而是操作系统的其他部分，因此，您需要了解 Apc 的工作方式。

Windows 操作系统使用三种类型的 Apc：

-   *用户 apc* 仅在用户模式下运行，并且仅在当前线程处于可报警等待状态时运行。 操作系统使用用户 Apc 来实现重叠 i/o 和 **QueueUserApc** Win32 例程等机制。

-   *正常内核 apc* 在内核模式下运行，以 IRQL = 被动 \_ 级别。 普通内核 APC 抢先于所有用户模式代码，包括用户 Apc。 普通内核 Apc 通常由文件系统和文件系统筛选器驱动程序使用。

-   *特殊内核 apc* 在内核模式下运行，以 IRQL = APC \_ 级别。 一种特殊的内核 APC 抢先于用户模式代码和内核模式代码，以 IRQL = 被动 \_ 级别执行，其中包括用户 apc 和普通内核 apc。 操作系统使用特殊内核 Apc 来处理 i/o 请求完成等操作。

 

 




