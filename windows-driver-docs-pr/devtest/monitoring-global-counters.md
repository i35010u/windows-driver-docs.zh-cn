---
title: 监视全局计数器
description: 监视全局计数器
keywords:
- 全局计数器 WDK 驱动程序验证程序
- 驱动程序验证程序 WDK，计数器
- 统计信息 WDK 驱动程序验证程序
- 计数器 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df5d1a35b47714c0c68686751550448fc426164e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819715"
---
# <a name="monitoring-global-counters"></a>监视全局计数器


## <span id="ddk_monitoring_global_counters_tools"></span><span id="DDK_MONITORING_GLOBAL_COUNTERS_TOOLS"></span>


*全局计数器* 是监视驱动程序验证程序对驱动程序执行的某些操作的统计信息。 这些统计信息是从要验证的所有驱动程序中提取的。

全局计数器可以通过使用 [**验证程序命令行**](verifier-command-line.md)或使用驱动程序验证器管理器来查看。 驱动程序验证器管理器有两个版本-一个适用于 [windows 2000](driver-verifier-manager--windows-2000-.md) ，一个用于 [windows XP 和更高](driver-verifier-manager--windows-xp-and-later-.md)版本。

### <a name="span-idverifier_command_linespanspan-idverifier_command_linespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要查看全局计数器，请使用 **verifier/query** 命令。 这将显示全局计数器和 [单个计数器](monitoring-individual-counters.md)。

驱动程序验证程序 [日志文件](creating-log-files.md)中也包含全局计数器。

### <a name="span-iddriver_verifier_manager__windows_2000_spanspan-iddriver_verifier_manager__windows_2000_spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证器管理器 (Windows 2000) 

若要查看全局计数器，请选择 " **全局计数器** " 选项卡。此选项卡几乎包括所有全局计数器。  (但是，" **未跟踪的分配** " 计数器位于 " **池跟踪** " 屏幕上，"95%" 特殊池警报位于 " **驱动程序状态** " 屏幕上，如下所述。 ) 

### <a name="span-iddriver_verifier_manager__windows_xp_and_later_spanspan-iddriver_verifier_manager__windows_xp_and_later_spandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证器管理器 (Windows XP 和更高版本) 

若要查看全局计数器，请启动驱动程序验证程序管理器，并选择 **显示有关当前已验证的驱动程序** 任务的信息。 然后按两次 " **下一步** "。

### <a name="span-idexplanation_of_global_countersspanspan-idexplanation_of_global_countersspanexplanation-of-global-counters"></a><span id="explanation_of_global_counters"></span><span id="EXPLANATION_OF_GLOBAL_COUNTERS"></span>全局计数器的说明

以下全局计数器监视与 " [强制 IRQL 检查](force-irql-checking.md) " 选项相关的统计信息。 这些计数器包括自上次启动以来由当前正在验证的所有内核模式驱动程序执行的操作。

<span id="IRQL_Raises"></span><span id="irql_raises"></span><span id="IRQL_RAISES"></span>**IRQL 引发**  
验证的驱动程序引发了 IRQL 的次数。

<span id="Spinlocks_Acquired"></span><span id="spinlocks_acquired"></span><span id="SPINLOCKS_ACQUIRED"></span>**已获取旋转锁**  
验证驱动程序获取的自旋锁的次数。

<span id="Executions_Synchronized"></span><span id="executions_synchronized"></span><span id="EXECUTIONS_SYNCHRONIZED"></span>**已同步执行**  
经验证的驱动程序使用与给定中断对象指针关联的 ISR 同步给定例程的执行次数。

<span id="Trims"></span><span id="trims"></span><span id="TRIMS"></span>**修剪**  
驱动程序验证器从工作集中修整可分页内存的次数。  (请注意，这是驱动程序验证器执行的修整传递数，而不是已修整的页数。 ) 

以下全局计数器监视与 [低资源模拟](low-resources-simulation.md) 选项相关的统计信息。

<span id="Faults_Injected"></span><span id="faults_injected"></span><span id="FAULTS_INJECTED"></span>**注入的故障**  
自上次启动以来，驱动程序验证程序特意失败的资源分配总数。

以下全局计数器监视与 [特殊池](special-pool.md) 选项相关的统计信息。 这些计数器始终反映自上次由当前正在验证的所有内核模式驱动程序启动以来尝试的分配。

<span id="Pool_Allocations_Attempted"></span><span id="pool_allocations_attempted"></span><span id="POOL_ALLOCATIONS_ATTEMPTED"></span>**已尝试池分配**  
这些驱动程序尝试的内存分配总数。

<span id="Pool_Allocations_Succeeded"></span><span id="pool_allocations_succeeded"></span><span id="POOL_ALLOCATIONS_SUCCEEDED"></span>**池分配成功**  
成功的分配尝试数。

<span id="Pool_Allocations_Succeeded_in_Special_Pool"></span><span id="pool_allocations_succeeded_in_special_pool"></span><span id="POOL_ALLOCATIONS_SUCCEEDED_IN_SPECIAL_POOL"></span>**已成功在特殊池分配池**  
成功和从特殊池中分配的分配尝试数。

<span id="Pool_Allocations_Without_Tag"></span><span id="pool_allocations_without_tag"></span><span id="POOL_ALLOCATIONS_WITHOUT_TAG"></span>**无标记的池分配**  
这些驱动程序请求内存分配但未提供池标记的次数。 对于每个分配，始终建议 (池标记。 ) 

<span id="Pool_Allocations_Failed"></span><span id="pool_allocations_failed"></span><span id="POOL_ALLOCATIONS_FAILED"></span>**池分配失败**  
由于内存不足而失败的分配尝试次数。

如果启用了 "特殊池" 功能，但尚未从特殊池分配所有池分配的95%，则会出现警告。 在 Windows XP 和更高版本中，此警告会出现在 **全局计数器** 屏幕上的对话框中。 在 Windows 2000 中，此警告将显示在 " **驱动程序状态** " 屏幕上。

以下全局计数器监视与 [特殊池](special-pool.md) 和 [池跟踪](pool-tracking.md) 选项相关的统计信息。 如果池跟踪不处于活动状态，则它将始终为零。

<span id="Pool_Allocations_Not_Tracked"></span><span id="pool_allocations_not_tracked"></span><span id="POOL_ALLOCATIONS_NOT_TRACKED"></span>**未跟踪池分配**  
当前正在验证的所有驱动程序的未跟踪分配数。 大小为一页或更大的分配不会被池跟踪跟踪，无法从特殊池进行分配。 [单个计数器](monitoring-individual-counters.md)不反映这些分配。  (在 Windows 2000 中，可以在 "**未跟踪** 的标题" 标题下的 "**池跟踪**" 屏幕上找到此计数器。 ) 

 

 





