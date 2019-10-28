---
title: 快速互斥锁和受保护互斥锁
description: 快速互斥锁和受保护互斥锁
ms.assetid: 8c8014bf-6b81-4039-ae93-d4cedd6d6fed
keywords:
- 同步 WDK 内核，快速 mutex
- 同步 WDK 内核，受保护的 mutex
- 受保护的 mutex WDK 内核
- 快速互斥体 WDK 内核
- mutex WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4139553213606144b0559b725fb23adeafb80c4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838693"
---
# <a name="fast-mutexes-and-guarded-mutexes"></a>快速互斥锁和受保护互斥锁


从 Windows 2000 开始，驱动程序可以使用*快速互斥*体，前提是对于在 IRQL &lt;= APC\_级别运行的代码，它们需要一种低开销形式的互斥。 快速 mutex 可以保护一次只能由一个线程输入的代码路径。 若要输入受保护的代码路径，线程将*获取*互斥体。 如果另一个线程已获取互斥体，则会挂起当前线程的执行，直到释放互斥体。 若要退出受保护的代码路径，该线程将*释放*该互斥体。

从 Windows Server 2003 开始，驱动程序还可以使用*受保护的 mutex*。 受保护的 mutex 是用于快速 mutex 的下拉替换，但提供更好的性能。 与快速 mutex 一样，受保护的 mutex 可以保护一次只能由一个线程输入的代码路径。 但是，使用受保护的 mutex 的代码的运行速度比使用快速 mutex 的代码更快。

在 Windows 8 之前的 Windows 版本中，受保护的互斥体实现方式与快速互斥体不同。 通过快速 mutex 保护的代码路径以 IRQL = APC\_级别运行。 受保护的 mutex 保护的代码路径将以 IRQL &lt;= APC\_级别运行，但所有 Apc 都处于禁用状态。 在这些早期版本的 Windows 中，获取受保护的 mutex 比获取快速 mutex 更快。 但是，这两种类型的 mutex 的行为是相同的，并且受到相同的限制。 特别是，不能从不是以 IRQL = APC\_级别调用的内核例程，也不能从由快速 mutex 或受保护的 mutex 保护的代码路径调用。

从 Windows 8 开始，受保护的 mutex 作为快速互斥体实现。 在受受保护的 mutex 或快速 mutex 保护的代码路径中，[驱动程序验证](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)器会将对内核例程的调用视为 IRQL = APC\_级别。 与 Windows 的早期版本一样，在 APC\_级别非法的调用在受保护的 mutex 或快速 mutex 保护的代码路径中是非法的。

### <a name="fast-mutexes"></a>快速 Mutex

快速 mutex 由[**fast\_mutex**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构表示。 驱动程序为**FAST\_MUTEX**结构分配其自己的存储，然后调用[**ExInitializeFastMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializefastmutex)例程来初始化该结构。

线程通过执行以下操作之一来获取快速 mutex：

-   调用[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))例程。 如果已由另一个线程获取互斥体，则会挂起调用线程的执行，直到互斥体可用。

-   调用[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))例程以尝试获取快速 mutex，而不挂起当前线程。 例程会立即返回，而不管是否已获取互斥体。 如果**ExTryToAcquireFastMutex**成功获取调用方的 mutex，则返回**TRUE** ; 否则返回 false。否则，返回**FALSE**。

线程调用[**ExReleaseFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545549(v=vs.85))来释放由**ExAcquireFastMutex**或**ExTryToAcquireFastMutex**获取的快速 mutex。

通过快速 mutex 保护的代码路径以 IRQL = APC\_级别运行。 **ExAcquireFastMutex**和**ExTryToAcquireFastMutex**会将当前的 irql 提高到 APC\_级别， **EXRELEASEFASTMUTEX**将还原原始的 irql。 因此，当线程包含快速 mutex 时，所有 Apc 都处于禁用状态。

如果保证代码路径始终在 APC\_级别运行，则驱动程序可以改为调用[**ExAcquireFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544340(v=vs.85))和[**ExReleaseFastMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545567(v=vs.85))以获取和释放快速 mutex。 这些例程不会更改当前的 IRQL，只能在当前 IRQL 为 APC\_级别时安全地使用。

无法以递归方式获取快速 mutex。 如果已保持快速互斥体的线程尝试获取该线程，该线程将死锁。 快速 mutex 只能在以 IRQL &lt;= APC\_级别运行的代码中使用。

### <a name="guarded-mutexes"></a>受保护的 Mutex

受保护的互斥体（从 Windows Server 2003 开始可用）与快速互斥体执行相同的功能，但性能更高。

从 Windows 8 开始，受保护的互斥体和快速 mutex 的实现方式相同。

在 Windows 8 之前的 Windows 版本中，受保护的互斥体实现方式与快速互斥体不同。 获取快速 mutex 会将当前的 IRQL 提高到 APC\_级别，同时获取受保护的互斥体将进入受保护的区域，这是一个速度更快的操作。 有关受保护区域的详细信息，请参阅[关键区域和受保护区域](critical-regions-and-guarded-regions.md)。

受保护的 mutex 由[**KGUARDED\_mutex**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构表示。 驱动程序为**KGUARDED\_MUTEX**结构分配其自己的存储，然后调用[**KeInitializeGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeguardedmutex)例程来初始化该结构。

线程通过执行以下操作之一来获取受保护的互斥体：

-   调用[**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))。 如果已由另一个线程获取互斥体，则会挂起调用线程的执行，直到互斥体可用。

-   调用[**KeTryToAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553307)以尝试获取受保护的 mutex，而不挂起当前线程。 例程会立即返回，而不管是否已获取互斥体。 如果**KeTryToAcquireGuardedMutex**成功获取调用方的 mutex，则返回**TRUE** ; 否则返回 false。否则，返回**FALSE**。

线程调用[**KeReleaseGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutex)来释放由**KeAcquireGuardedMutex**或**KeTryToAcquireGuardedMutex**获取的受保护互斥体。

保存受保护互斥体的线程将在受保护区域内隐式运行。 **KeAcquireGuardedMutex**和**KeTryToAcquireGuardedMutex**输入受保护的区域， **KeReleaseGuardedMutex**将其退出。 当线程持有受保护的 mutex 时，所有 Apc 都处于禁用状态。

如果保证在禁用所有 Apc 后运行代码路径，则驱动程序可以改为使用[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))和[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)获取和释放受保护的 mutex。 这些例程不会进入或退出受保护的区域，并且只能在已存在的受保护区域内或 IRQL = APC\_级别使用。

不能以递归方式获取受保护的互斥体。 如果已持有受保护互斥体的线程尝试获取该线程，该线程将死锁。 受保护的 mutex 只能在以 IRQL &lt;= APC\_级别运行的代码中使用。

 

 




