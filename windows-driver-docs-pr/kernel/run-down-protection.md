---
title: 停止运行保护
description: 从 Windows XP，run-down protection，可用于内核模式驱动程序。 驱动程序可以使用 run-down 保护可以安全地访问共享的系统内存，已创建和删除由另一个内核模式驱动程序中的对象。
ms.assetid: AF451636-DBA0-4905-9723-73EE7AA9483E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d43014655454b20629cdda877bcc7e0cb6f792f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567745"
---
# <a name="run-down-protection"></a>停止运行保护


从 Windows XP，run-down protection，可用于内核模式驱动程序。 驱动程序可以使用 run-down 保护可以安全地访问共享的系统内存，已创建和删除由另一个内核模式驱动程序中的对象。

一个对象称为*沿着*如果对象的未完成的所有访问都完成都后，将授予任何新请求来访问该对象。 例如，共享的对象可能需要向下运行，以便将其删除并替换为新对象。

该共享的对象所属的驱动程序可以启用其他驱动程序，以获取和释放的对象上的 run-down 保护。 完成 run-down 保护时生效，不是所有者的驱动程序可以访问该对象没有所有者，将删除的对象之前访问的风险。 访问启动之前，访问驱动程序请求的对象上的 run-down 保护。 对于生存期较长的对象，几乎始终授予此请求。 访问完成后，访问驱动程序将释放对象上的其以前已获得 run-down 保护。

## <a name="primary-run-down-protection-routines"></a>主 run-down 保护例程


若要开始共享对象，该对象所属的驱动程序调用[ **ExInitializeRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569373)例程，以初始化对象上的 run-down 保护。 此调用后，访问该对象的其他驱动程序可以获取和释放的对象上的 run-down 保护。

访问共享的对象调用的驱动程序[ **ExAcquireRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569371)例程到对象上请求 run-down 保护。 完成访问后，此驱动程序会调用[ **ExReleaseRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569375)例程来释放该对象上的 run-down 保护。

如果所属的驱动程序确定必须删除该共享的对象，该驱动程序等待对象的未完成的所有访问都完成后删除该对象。

若要删除的共享的对象的准备，在所属的驱动程序将调用[ **ExWaitForRundownProtectionRelease** ](https://msdn.microsoft.com/library/windows/hardware/jj569378)例程，以等待对象向下运行。 在此调用期间**ExWaitForRundownProtectionRelease**等待所有以前授予的 run-down 保护的对象被释放，但可防止针对 run-down 保护的对象上的新请求授予。 最后一个受保护的访问完成并且 run-down 保护的所有实例会被都释放后, **ExWaitForRundownProtectionRelease**退货和所属的驱动程序可以安全地删除对象。

**ExWaitForRundownProtectionRelease**阻止调用驱动程序线程的执行，直到保存 run-down 保护了共享对象的所有驱动程序发布这种保护。 若要防止**ExWaitForRundownProtectionRelease**阻止过长时间的执行访问共享的对象的驱动程序线程应避免被挂起时它们在对象上具有 run-down 保护。 出于此原因，访问驱动程序应调用**ExAcquireRundownProtection**并**ExReleaseRundownProtection**临界区或受保护的区域内或同时运行在 IRQL = APC\_级别。

## <a name="uses-for-run-down-protection"></a>用于 run-down 保护


Run-down 保护是一个共享对象，几乎始终是可用的但有时可能需要删除并替换为对提供访问特别有用。 访问数据或调用此对象中的例程必须不尝试访问的对象，其被删除后的驱动程序。 否则，这些无效的访问可能会导致不可预知的行为、 数据损坏或即使系统出现故障。

例如，防病毒驱动程序通常会保留在内存中加载时运行的操作系统。 有时，此驱动程序可能需要卸载并替换为驱动程序的更新版本。 其他驱动程序将 I/O 请求发送到的防病毒的驱动程序，用于访问数据和此驱动程序中的例程。 在发送前的 I/O 请求，内核组件，如文件系统筛选器管理器，可以获取 run-down 保护以防止出现过早卸载的防病毒驱动程序时它处理 I/O 请求。 I/O 请求完成后，可以释放 run-down 保护。

Run-down 保护不会序列化到共享对象的访问。 如果两个或多个访问驱动程序可以同时按住 run-down 保护一个对象，并且必须序列化对对象的访问，必须使用其他机制，如相互排斥锁定要序列化访问。

## <a name="the-exrundownref-structure"></a>EX\_断开\_REF 结构


[ **EX\_断开\_REF** ](https://msdn.microsoft.com/library/windows/hardware/jj569379)结构上的共享对象跟踪的 run-down 保护的状态。 此结构是不透明的驱动程序。 系统提供 run-down 保护例程使用此结构的 run-down 保护生效目前对对象的实例数进行计数。 这些例程使用此结构来跟踪该对象向下运行还是在过程中向下运行。

若要开始共享对象，该对象所属的驱动程序调用**ExInitializeRundownProtection**来初始化**EX\_断开\_REF**与关联的结构对象。 初始化之后，拥有驱动程序可以提供此结构其他驱动程序的需要对对象的访问。 访问驱动程序将此结构作为参数传递**ExAcquireRundownProtection**并**ExReleaseRundownProtection**调用的获取和释放的对象上的 run-down 保护。 所属的驱动程序将此结构作为参数传递**ExWaitForRundownProtectionRelease**等待要向下运行，以便可以安全删除的对象的调用。

## <a name="comparison-to-locks"></a>与锁之间的比较


Run-down 保护是其中一种以保证对共享对象的安全访问。 另一种方法是使用互斥软件锁定。 如果驱动程序需要访问当前已由另一个驱动程序的对象，第一个驱动程序必须等待第二个的驱动程序才能释放锁。 但是，获取和释放锁可能成为性能瓶颈，并且锁可以占用大量的内存。 如果使用不正确，锁可能会导致相同的共享对象成为死锁争用的驱动程序。 为了检测和避免死锁通常需要大量计算资源所。

与锁，相比 run-down protection 具有相对轻量的处理时间和内存要求。 与要确保删除对象会推迟，直到完成所有未完成访问的对象的对象相关联的简单引用计数。 使用此方法时，原子，互锁的硬件指令可用而不是相互排斥软件锁来保证安全访问的对象。 调用以获取和释放 run-down 保护是通常速度很快。 使用轻量的机制，如 run-down 保护的好处可能很大的长的有效期，并在许多驱动程序之间共享的共享对象。

## <a name="other-run-down-protection-routines"></a>其他 run-down 保护例程


其他几个 run-down 保护例程都可用，除了前面所述。 某些驱动程序可能会使用这些其他例程。

[ **ExReInitializeRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569374)例程使以前用[ **EX\_断开\_REF** ](https://msdn.microsoft.com/library/windows/hardware/jj569379)结构要与新对象相关联，并初始化此对象上的 run-down 保护。

[ **ExRundownCompleted** ](https://msdn.microsoft.com/library/windows/hardware/jj569377)例行更新**EX\_断开\_REF**结构，指示关联的对象的向下运行已完成。

[ **ExAcquireRundownProtectionEx** ](https://msdn.microsoft.com/library/windows/hardware/jj569372)并[ **ExReleaseRundownProtectionEx** ](https://msdn.microsoft.com/library/windows/hardware/jj569376)例程是类似于[ **ExAcquireRundownProtection** ](https://msdn.microsoft.com/library/windows/hardware/jj569371)并[ **ExReleaseRundownProtection**](https://msdn.microsoft.com/library/windows/hardware/jj569375)。 以下四种例程中递增或递减的 run-down 保护实例实际上对共享对象的计数。 而**ExAcquireRundownProtection**并**ExReleaseRundownProtection**递增和递减 1，此计数**ExAcquireRundownProtectionEx**并**ExReleaseRundownProtectionEx**递增和递减的任意量的计数。

 

 




