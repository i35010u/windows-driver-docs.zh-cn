---
title: 监视全局计数器
description: 监视全局计数器
ms.assetid: ca8f2b87-bb62-4389-bd59-1ed8ef6ac730
keywords:
- 全局计数器 WDK Driver Verifier
- 驱动程序验证程序 WDK 计数器
- WDK 驱动程序验证程序的统计信息
- 计数器 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d248ae19b177ce8a55003bf7387dcabcda823fcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391324"
---
# <a name="monitoring-global-counters"></a>监视全局计数器


## <span id="ddk_monitoring_global_counters_tools"></span><span id="DDK_MONITORING_GLOBAL_COUNTERS_TOOLS"></span>


*全局计数器*监视某些驱动程序验证程序的驱动程序执行的操作的统计信息。 这些统计信息是来自正在验证的所有驱动程序。

可以通过查看全局计数器[**验证程序命令行**](verifier-command-line.md)，或通过使用驱动程序验证程序管理器。 有两个版本的驱动程序验证程序管理器-一个用于[Windows 2000](driver-verifier-manager--windows-2000-.md) ，另一个用于[Windows XP 及更高版本](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要查看全局计数器，请使用**verifier /query**命令。 这将显示两个全局计数器并[各个计数器](monitoring-individual-counters.md)。

全局计数器也包括在 Driver Verifier[日志文件](creating-log-files.md)。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证程序管理器 (Windows 2000)

若要查看全局计数器，请选择**全局计数器**选项卡。此选项卡包括几乎所有全局计数器。 (但是，**不跟踪分配**计数器位于**池跟踪**屏幕和 95%的特殊池警报位于**驱动程序状态**屏幕上，如所述下一行。）

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证程序管理器 (Windows XP 及更高版本)

若要查看全局计数器，请启动驱动程序验证程序管理器，并选择**显示有关当前已验证的驱动程序信息**任务。 然后按**下一步**两次。

### <a name="span-idexplanationofglobalcountersspanspan-idexplanationofglobalcountersspanexplanation-of-global-counters"></a><span id="explanation_of_global_counters"></span><span id="EXPLANATION_OF_GLOBAL_COUNTERS"></span>全局计数器的说明

以下全局计数器监视到相关的统计信息[Force IRQL 检查](force-irql-checking.md)选项。 这些计数器包括自上次启动以来执行的所有内核模式驱动程序的当前正在验证操作。

<span id="IRQL_Raises"></span><span id="irql_raises"></span><span id="IRQL_RAISES"></span>**IRQL 引发**  
已验证的次数，驱动程序引发的 IRQL。

<span id="Spinlocks_Acquired"></span><span id="spinlocks_acquired"></span><span id="SPINLOCKS_ACQUIRED"></span>**获取的自旋锁**  
验证驱动程序获取自旋锁的次数的编号。

<span id="Executions_Synchronized"></span><span id="executions_synchronized"></span><span id="EXECUTIONS_SYNCHRONIZED"></span>**执行已同步**  
次数验证驱动程序与给定的中断对象指针与关联 ISR 同步执行给定例程。

<span id="Trims"></span><span id="trims"></span><span id="TRIMS"></span>**修剪**  
Driver Verifier 裁剪从工作集中的可分页内存次数。 （请注意，这是若干修整传递所做的驱动程序验证程序，不剪裁的页面数。）

以下全局计数器监视与相关的统计信息[低资源模拟](low-resources-simulation.md)选项。

<span id="Faults_Injected"></span><span id="faults_injected"></span><span id="FAULTS_INJECTED"></span>**故障注入**  
资源分配失败有意驱动程序验证程序自上次启动以来的总数。

以下全局计数器监视到相关的统计信息[特殊池](special-pool.md)选项。 这些计数器始终反映自上次启动以来尝试的当前正在验证的所有内核模式驱动程序的分配。

<span id="Pool_Allocations_Attempted"></span><span id="pool_allocations_attempted"></span><span id="POOL_ALLOCATIONS_ATTEMPTED"></span>**池分配已尝试**  
尝试这些驱动程序的内存分配的总数。

<span id="Pool_Allocations_Succeeded"></span><span id="pool_allocations_succeeded"></span><span id="POOL_ALLOCATIONS_SUCCEEDED"></span>**池分配成功**  
分配的编号尝试成功安装。

<span id="Pool_Allocations_Succeeded_in_Special_Pool"></span><span id="pool_allocations_succeeded_in_special_pool"></span><span id="POOL_ALLOCATIONS_SUCCEEDED_IN_SPECIAL_POOL"></span>**池分配特殊池中成功**  
已成功，然后从特殊池中分配的分配尝试次数。

<span id="Pool_Allocations_Without_Tag"></span><span id="pool_allocations_without_tag"></span><span id="POOL_ALLOCATIONS_WITHOUT_TAG"></span>**没有标记的池分配**  
数倍这些驱动程序请求的内存分配，但没有提供池标记。 （池标记始终建议每次分配。）

<span id="Pool_Allocations_Failed"></span><span id="pool_allocations_failed"></span><span id="POOL_ALLOCATIONS_FAILED"></span>**池分配失败**  
分配失败的尝试，由于内存不足的数。

如果启用了特殊池功能，但从特殊的池已分配给不超过 95%的池的所有分配，将显示一条警告。 在 Windows XP 及更高版本，此警告将显示在对话框中对**全局计数器**屏幕。 在 Windows 2000 中，会出现此警告上**驱动程序状态**屏幕。

以下全局计数器监视与相关的统计信息[特殊池](special-pool.md)并[池跟踪](pool-tracking.md)选项。 如果池跟踪未处于活动状态，它将始终为零。

<span id="Pool_Allocations_Not_Tracked"></span><span id="pool_allocations_not_tracked"></span><span id="POOL_ALLOCATIONS_NOT_TRACKED"></span>**池分配不会跟踪**  
从当前正在验证的所有驱动程序的未跟踪分配数。 其大小不是一个页面或更大的分配池跟踪由跟踪，并且不能从特殊池分配。 [各个计数器](monitoring-individual-counters.md)不会反映这些分配。 (在 Windows 2000 中，可以上找到此计数器**池跟踪**标题下的屏幕**不跟踪分配**。)

 

 





