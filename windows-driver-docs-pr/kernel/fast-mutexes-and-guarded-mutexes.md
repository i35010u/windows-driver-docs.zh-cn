---
title: 快速互斥锁和受保护互斥锁
description: 快速互斥锁和受保护互斥锁
ms.assetid: 8c8014bf-6b81-4039-ae93-d4cedd6d6fed
keywords:
- 同步 WDK 内核，快速 mutex
- 同步 WDK 内核，受保护的互斥锁
- 受保护的互斥体 WDK 内核
- 快速互斥体，WDK 内核
- 互斥体，WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 212263c52417da6fcbe0ba80ffb3e8b347c59d82
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359969"
---
# <a name="fast-mutexes-and-guarded-mutexes"></a>快速互斥锁和受保护互斥锁


从 Windows 2000 开始，可以使用驱动程序*快速 mutex*如果他们需要在 IRQL 运行的代码的开销较低的形式的互斥&lt;= APC\_级别。 快速的互斥体可以保护一次只有一个线程必须输入的代码路径。 若要输入的受保护的代码路径，该线程*获取*互斥体。 如果另一个线程已获取互斥体，直到释放互斥体挂起当前线程的执行。 若要退出受保护的代码路径，该线程*释放*互斥体。

从 Windows Server 2003 开始，驱动程序还可以使用*受保护的互斥体*。 受保护的互斥体是随时取代快速互斥体，但提供更好的性能。 一个快速的互斥体，如受保护的互斥体可以保护一次只有一个线程必须输入的代码路径。 但是，代码使用受保护的互斥体，运行速度比使用快速互斥体的代码。

在版本的 Windows 8 之前的 Windows 中，受保护的互斥体是从快速互斥体以不同的方式实现。 受快速互斥体的代码路径运行在 IRQL = APC\_级别。 保护的受保护的互斥体的代码路径运行在 IRQL &lt;= APC\_级别但与所有 Apc 禁用。 在这些早期版本的 Windows 中，获取受保护的互斥体是比快速互斥体获取更快地操作。 但是，这两种类型的互斥体的行为方式相同，并且受到相同限制。 具体而言，内核例程的是非法的 IRQL 在调用 = APC\_不应从受快速互斥体或受保护的互斥体的代码路径调用级别。

从 Windows 8 开始，受保护的互斥体作为快速互斥体实现。 在受保护的互斥锁或快速的互斥体，通过受保护的代码路径[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)将调用内核例程作为发生在 IRQL = APC\_级别。 与早期版本的 Windows，是在 APC 非法的调用\_级别是非法的保护的受保护的互斥锁或快速的互斥体的代码路径中。

### <a name="fast-mutexes"></a>快速 Mutex

快速的互斥体为由[**快速\_互斥体**](https://msdn.microsoft.com/library/windows/hardware/ff545715)结构。 该驱动程序会将有关存储分配**快速\_MUTEX**结构，然后调用[ **ExInitializeFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff545293)例程初始化结构。

一个线程获得快速互斥体通过执行以下任一操作：

-   调用[ **ExAcquireFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff544337)例程。 如果已由另一个线程获取互斥体，直到获得该互斥体挂起调用线程的执行。

-   调用[ **ExTryToAcquireFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff545647)例程，以尝试获取快速互斥体，而不会挂起当前线程。 例程将立即返回而不考虑是否已获取互斥体。 **ExTryToAcquireFastMutex**将返回**TRUE**如果成功获取互斥体的调用方; 否则，它将返回**FALSE**。

线程调用[ **ExReleaseFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff545549)释放已通过以下任一方法获取快速互斥体**ExAcquireFastMutex**或**ExTryToAcquireFastMutex**.

受快速互斥体的代码路径运行在 IRQL = APC\_级别。 **ExAcquireFastMutex**并**ExTryToAcquireFastMutex**引发 APC 为当前 IRQL\_级别，并**ExReleaseFastMutex**还原原始的 IRQL。 因此，线程持有快速互斥体时，将禁用所有 Apc。

如果代码路径可确保始终运行在 APC\_级别，该驱动程序可以改为调用[ **ExAcquireFastMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff544340)并[ **ExReleaseFastMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff545567)来获取和释放快速互斥体。 这些例程不更改当前 IRQL，并且可以安全地使用当前 IRQL 时才 APC\_级别。

快速互斥体，不能是递归获得。 如果已经持有快速互斥锁的线程试图获得该软件，该线程将发生死锁。 可以在 IRQL 运行的代码中仅使用互斥体，快速&lt;= APC\_级别。

### <a name="guarded-mutexes"></a>受保护的互斥锁

受保护互斥体是从 Windows Server 2003 开始提供，执行相同的功能快速互斥体，但更高的性能。

从 Windows 8 开始，受保护的互斥锁和互斥体，快速实现完全相同。

在版本的 Windows 8 之前的 Windows 中，受保护的互斥体是从快速互斥体以不同的方式实现。 获取快速互斥体引发 APC 为当前 IRQL\_级别，而获取受保护的互斥体进入受保护的区域，这是一个更快的操作。 有关受保护区域的详细信息，请参阅[临界区和受保护区域](critical-regions-and-guarded-regions.md)。

受保护的互斥体为由[ **KGUARDED\_互斥体**](https://msdn.microsoft.com/library/windows/hardware/ff554235)结构。 该驱动程序会将有关存储分配**KGUARDED\_MUTEX**结构，然后调用[ **KeInitializeGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff552144)例程，以初始化结构。

一个线程获得受保护的互斥体，通过执行以下任一操作：

-   调用[ **KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)。 如果已由另一个线程获取互斥体，直到获得该互斥体挂起调用线程的执行。

-   调用[ **KeTryToAcquireGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553307)尝试而不会挂起当前线程获取受保护的互斥体。 例程将立即返回而不考虑是否已获取互斥体。 **KeTryToAcquireGuardedMutex**将返回**TRUE**如果成功获取互斥体的调用方; 否则，它将返回**FALSE**。

线程调用[ **KeReleaseGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553124)释放已通过以下任一方法获取受保护的互斥体**KeAcquireGuardedMutex**或**KeTryToAcquireGuardedMutex**。

隐式持有受保护的互斥体的线程在受保护区域中运行。 **KeAcquireGuardedMutex**并**KeTryToAcquireGuardedMutex**输入的受保护的区域，而**KeReleaseGuardedMutex**退出它。 禁用所有 Apc 线程保留受保护的互斥体。

如果代码路径可得到保证，若要运行具有禁用所有 Apc，驱动程序可以使用[ **KeAcquireGuardedMutexUnsafe** ](https://msdn.microsoft.com/library/windows/hardware/ff551894)并[ **KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)来获取和释放受保护的互斥体。 这些例程不输入或退出受保护的区域和可以使用仅在现有的已受保护区域内或在 IRQL = APC\_级别。

受保护的互斥锁不能是递归获得。 如果线程已持有受保护的互斥体尝试以获得该软件，该线程将发生死锁。 可以在 IRQL 运行的代码中仅使用受保护的互斥锁&lt;= APC\_级别。

 

 




