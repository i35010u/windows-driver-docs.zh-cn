---
title: 停止运行保护
description: 从 Windows XP 开始，内核模式驱动程序提供了运行时保护。 驱动程序可以使用运行时保护来安全地访问共享系统内存中的对象，这些对象由另一个内核模式驱动程序创建和删除。
ms.assetid: AF451636-DBA0-4905-9723-73EE7AA9483E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fdd043fe695b3ca8077921552c48ff3824ef3f72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838443"
---
# <a name="run-down-protection"></a>停止运行保护


从 Windows XP 开始，内核模式驱动程序提供了运行时保护。 驱动程序可以使用运行时保护来安全地访问共享系统内存中的对象，这些对象由另一个内核模式驱动程序创建和删除。

如果对象的所有未完成访问都已完成，并且没有访问该对象的新请求，则称该对象处于*关闭*状态。 例如，共享对象可能需要关闭才能删除并替换为新的对象。

拥有共享对象的驱动程序可以允许其他驱动程序获取和释放对象的运行时保护。 当运行时保护生效时，所有者以外的其他驱动程序可以访问该对象，而在访问完成之前，所有者将删除该对象。 在访问开始之前，访问驱动程序请求对对象的运行时保护。 对于生存期较长的对象，几乎总是授予此请求。 访问完成后，访问驱动程序将释放其以前获取的对对象的运行时保护。

## <a name="primary-run-down-protection-routines"></a>主运行时保护例程


若要开始共享某个对象，拥有该对象的驱动程序将调用[**ExInitializeRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializerundownprotection)例程来初始化该对象的运行时保护。 此调用之后，访问对象的其他驱动程序可以获取和释放对象的运行时保护。

访问共享对象的驱动程序将调用[**ExAcquireRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirerundownprotection)例程来请求对对象的运行时保护。 访问完成后，该驱动程序将调用[**ExReleaseRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaserundownprotection)例程以释放对对象的运行时保护。

如果拥有的驱动程序确定必须删除共享对象，则此驱动程序将等待删除对象，直到对象的所有未完成的访问都完成。

在准备删除共享对象时，拥有的驱动程序会调用[**ExWaitForRundownProtectionRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exwaitforrundownprotectionrelease)例程以等待该对象运行。 在此调用过程中， **ExWaitForRundownProtectionRelease**将等待要释放的对象上的所有之前授予的运行时保护实例，但会阻止对对象的运行时保护的新请求被授予。 最后一个受保护的访问完成并且发布所有运行时保护实例后， **ExWaitForRundownProtectionRelease**将返回，并且拥有的驱动程序可以安全删除该对象。

**ExWaitForRundownProtectionRelease**阻止调用驱动程序线程的执行，直到对共享对象拥有运行时保护的所有驱动程序释放此保护。 若要防止**ExWaitForRundownProtectionRelease**长时间阻塞执行，则访问共享对象的驱动程序线程应避免在对对象拥有运行保护时挂起。 出于此原因，访问驱动程序应在关键区域或受保护的区域内或在 IRQL = APC\_级别下运行时调用**ExAcquireRundownProtection**和**ExReleaseRundownProtection** 。

## <a name="uses-for-run-down-protection"></a>用于运行时保护


运行时保护特别适用于提供对几乎始终可用但偶尔可能需要删除和替换的共享对象的访问权限。 在此对象中访问数据或调用例程的驱动程序在删除对象后，不能尝试访问它。 否则，这些无效访问可能会导致不可预知的行为、数据损坏，甚至可能导致系统故障。

例如，当操作系统正在运行时，防病毒驱动程序通常会在内存中保持加载状态。 有时，可能需要卸载此驱动程序，并将其替换为驱动程序的更新版本。 其他驱动程序将 i/o 请求发送到防病毒驱动程序，以访问此驱动程序中的数据和例程。 在发送 i/o 请求之前，内核组件（如文件系统筛选器管理器）可以获取运行时保护，以防止在处理 i/o 请求时过早卸载防病毒驱动程序。 I/o 请求完成后，可以释放运行时保护。

运行时保护不会序列化对共享对象的访问。 如果两个或更多访问驱动程序可以同时在某个对象上保持运行时保护，并且必须对对象的访问进行序列化，则必须使用某些其他机制（如互斥锁）来序列化访问。

## <a name="the-ex_rundown_ref-structure"></a>EX\_断开\_REF 结构


[**EX\_断开\_REF**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构跟踪共享对象上的运行时保护的状态。 此结构对于驱动程序是不透明的。 系统提供的运行时保护例程使用此结构来计算当前对对象有效的运行时保护实例的数目。 这些例程还使用此结构来跟踪对象是关闭的还是正在运行的进程。

若要开始共享某个对象，拥有该对象的驱动程序将调用**ExInitializeRundownProtection**来初始化与该对象关联的**EX\_断开\_REF**结构。 初始化后，拥有的驱动程序可以使此结构可供需要访问对象的其他驱动程序使用。 访问驱动程序将此结构作为参数传递给**ExAcquireRundownProtection**和**ExReleaseRundownProtection**调用，以便在对象上获取和释放运行时保护。 所属驱动程序将此结构作为参数传递给**ExWaitForRundownProtectionRelease**调用，以等待该对象运行，以便可以安全地将其删除。

## <a name="comparison-to-locks"></a>与锁的比较


运行时保护是保证对共享对象进行安全访问的几种方法之一。 另一种方法是使用相互排除的软件锁。 如果驱动程序需要访问当前由另一个驱动程序锁定的对象，则第一个驱动程序必须等待第二个驱动程序释放该锁。 但是，获取和释放锁可能会成为性能瓶颈，而锁可能会占用大量内存。 如果使用不正确，则锁定可能会导致争用相同共享对象的驱动程序被死锁。 检测和避免死锁的工作通常需要 diversion 的计算资源。

与锁相反，运行时保护的处理时间和内存要求相对较轻。 简单的引用计数与对象相关联，以确保在完成对象的所有未完成访问之前延迟对象删除。 使用此方法时，可以使用原子性的互锁硬件指令，而不是使用相互排除的软件锁来保证对对象的安全访问。 用于获取和释放运行时保护的调用通常速度非常快。 使用轻型机制的好处（如运行时保护）对于生存期很长且在多个驱动程序之间共享的共享对象非常重要。

## <a name="other-run-down-protection-routines"></a>其他运行时保护例程


除了前面提到的，还有其他几个运行时保护例程。 某些驱动程序可能会使用这些其他例程。

[**ExReInitializeRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializerundownprotection)例程使以前使用的[**EX\_断开\_REF**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构与新的对象相关联，并在此对象上初始化运行时保护。

[**ExRundownCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exrundowncompleted)例程将更新**EX\_断开\_REF**结构，以指示关联对象的运行已完成。

[**ExAcquireRundownProtectionEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirerundownprotectionex)和[**ExReleaseRundownProtectionEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaserundownprotectionex)例程类似于[**ExAcquireRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exacquirerundownprotection)和[**ExReleaseRundownProtection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaserundownprotection)。 这四个例程递增或递减在共享对象上生效的运行时保护实例的计数。 而**ExAcquireRundownProtection**和**ExReleaseRundownProtection**递增，并按1、 **ExAcquireRundownProtectionEx**和**ExReleaseRundownProtectionEx**递增和递减计数任意量。

 

 




