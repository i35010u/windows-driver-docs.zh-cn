---
title: 类型的 Apc
description: 类型的 Apc
ms.assetid: 74ed953c-1b2a-40b9-9df3-16869b198b38
keywords:
- 异步过程调用 WDK 内核
- Apc WDK 内核
- 用户 Apc WDK 内核
- 正常内核 Apc WDK 内核
- 特殊内核 Apc WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514f03879913030db26c5bfc094b394de2d9768e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525191"
---
# <a name="types-of-apcs"></a>类型的 Apc


异步过程调用 (APC) 是以异步方式执行的函数。 Apc 类似于延缓的过程调用 (Dpc)，但 Apc 特定线程的上下文中与 Dpc，不同的执行。 （而不是文件系统和文件系统筛选器驱动程序） 的驱动程序不使用 Apc 直接，但操作系统的其他部分执行操作，因此需要注意的 Apc 的工作原理。

Windows 操作系统使用 Apc 的三种：

-   *用户 Apc*严格在用户模式和仅当前线程处于可报警等待状态时运行。 操作系统使用用户 Apc 实现机制，例如重叠 I/O 并**QueueUserApc** Win32 例程。

-   *正常内核 Apc*运行在内核模式下在 IRQL = 被动\_级别。 正常内核 APC 抢先于所有用户模式代码，包括用户 Apc。 文件系统和文件系统筛选器驱动程序通常使用普通内核 Apc。

-   *特殊内核 Apc*运行在内核模式下在 IRQL = APC\_级别。 特殊内核 APC 抢先于用户模式代码和内核模式代码执行在 IRQL = 被动\_级别，包括用户 Apc 和正常内核 Apc。 操作系统使用特殊的内核 Apc 处理操作，如 I/O 请求完成。

 

 




