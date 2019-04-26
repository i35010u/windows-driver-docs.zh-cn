---
title: 编写 Bug 检查回调例程
description: 编写 Bug 检查回调例程
ms.assetid: 62aefe67-e197-4c45-b994-19bd7369dbc1
keywords:
- bug 检查回调例程 WDK 内核
- 回调例程 WDK bug 检查
- 注册回调例程
- KeRegisterBugCheckCallback
- BugCheckCallback
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66ef9c90be5fe83827ead362cdc813fd95870fdc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327334"
---
# <a name="writing-a-bug-check-callback-routine"></a>编写 Bug 检查回调例程





驱动程序可以注册时它会发出错误检查，则系统将执行的回调例程。

所有基于 NT 的操作系统上，可以使用驱动程序[ **KeRegisterBugCheckCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553105)例程，以注册[ *BugCheckCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540674)例程，并[ **KeDeregisterBugCheckCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551992)若要删除该例程。 驱动程序可以使用*BugCheckCallback*例程，以将其设备重置为已知状态。

在 Windows XP Service Pack 1 (SP1) 和 Windows Server 2003 之前, 的驱动程序也可以使用*BugCheckCallback*崩溃转储文件中存储数据： 系统调用每个*BugCheckCallback*例程之前写入崩溃转储文件，因此任何数据写入缓冲区传递给*BugCheckCallback*崩溃转储文件中存储。

在 Windows XP SP1 和 Windows Server 2003 及更高版本中，系统会调用*BugCheckCallback*写入崩溃转储文件后。 相反，系统支持两种其他类型的 bug 检查回调例程。 一个[ *BugCheckSecondaryDumpDataCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540679)例程可用于辅助数据写入崩溃转储文件。 一个[ *BugCheckDumpIoCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540677)例程可以用于将故障转储文件复制到设备。

在 Windows Server 2008 和更高版本的 Windows 中，可以实现一个驱动程序[ *BugCheckAddPagesCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540669)例程，以将特定于驱动程序的数据页添加到故障转储文件。 与不同*BugCheckSecondaryDumpDataCallback*例程，将数据追加到辅助崩溃转储区域， *BugCheckAddPagesCallback*例程会向崩溃转储区域中添加的数据页。 在调试期间，故障转储数据比更容易访问辅助崩溃转储数据。

驱动程序使用[ **KeRegisterBugCheckReasonCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff553110)并[ **KeDeregisterBugCheckReasonCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff552003)例程注册这三种*BugCheckXxxCallback*回调例程。

Bug 检查回调例程执行在 IRQL = 高\_级别，这会强制执行强限制可以执行的操作。

Bug 检查回调例程不能：

-   分配内存

-   访问可分页内存

-   使用任何同步机制

-   调用在 IRQL 必须执行的任何例程 = 调度\_级别或更低

Bug 检查回调例程保证运行而不发生中断，因此不需要进行同步。 （如果 bug 检查例程使用的任何同步机制，系统将发生死锁。）

可以安全地使用驱动程序的 bug 检查回调例程<strong>读取\_端口\_* XXX</strong><em>，**读取\_注册\_</em>XXX <strong><em>， 编写\_端口\_* XXX</strong><em>，以及**编写\_注册\_</em>XXX*** 例程与驱动程序的设备进行通信。 (有关这些例程的信息，请参阅[硬件抽象层例程](https://msdn.microsoft.com/library/windows/hardware/ff546644)。)

有关 bug 检查回叫的详细信息，请参阅[ *BugCheckCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540674)， [ *BugCheckAddPagesCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540669)， [*BugCheckDumpIoCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540677)， [ *BugCheckSecondaryDumpDataCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540679)，和[读取 Bug 检查回调数据](https://msdn.microsoft.com/library/windows/hardware/ff553558).

 

 




