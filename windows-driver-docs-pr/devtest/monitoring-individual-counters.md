---
title: 监视单个计数器
description: 监视单个计数器
keywords:
- 个别计数器 WDK 驱动程序验证程序
- 驱动程序验证程序 WDK，计数器
- 统计信息 WDK 驱动程序验证程序
- 计数器 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8853a793ce10e04f2dbd301dd9928717a0862b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819711"
---
# <a name="monitoring-individual-counters"></a>监视单个计数器


## <span id="ddk_monitoring_individual_counters_tools"></span><span id="DDK_MONITORING_INDIVIDUAL_COUNTERS_TOOLS"></span>


*单个计数器* 是监视驱动程序验证程序对驱动程序执行的某些操作的统计信息。 对于正在验证的每个驱动程序，这些统计信息将分别保留。

可以通过使用 [**验证程序命令行**](verifier-command-line.md)或使用驱动程序验证器管理器来查看单个计数器。 驱动程序验证器管理器有两个版本-一个适用于 [windows 2000](driver-verifier-manager--windows-2000-.md) ，一个用于 [windows XP 和更高](driver-verifier-manager--windows-xp-and-later-.md)版本。

### <a name="span-idverifier_command_linespanspan-idverifier_command_linespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要查看单个计数器，请使用 **verifier/query** 命令。 这将显示单个计数器和 [全局计数器](monitoring-global-counters.md)。

驱动程序验证程序 [日志文件](creating-log-files.md)中也包括各个计数器。

### <a name="span-iddriver_verifier_manager__windows_2000_spanspan-iddriver_verifier_manager__windows_2000_spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证器管理器 (Windows 2000) 

若要查看单个计数器，请选择 " **池跟踪** " 选项卡。然后从下拉框中选择所需的驱动程序。

### <a name="span-iddriver_verifier_manager__windows_xp_and_later_spanspan-iddriver_verifier_manager__windows_xp_and_later_spandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证器管理器 (Windows XP 和更高版本) 

若要查看单个计数器，请启动驱动程序验证程序管理器，并选择 " **显示有关当前已验证驱动程序的信息** " 任务。 然后按 " **下一步** " 三次。

最后，从下拉框中选择所需的驱动程序。

### <a name="span-idexplanation_of_individual_countersspanspan-idexplanation_of_individual_countersspanexplanation-of-individual-counters"></a><span id="explanation_of_individual_counters"></span><span id="EXPLANATION_OF_INDIVIDUAL_COUNTERS"></span>单个计数器的说明

单个计数器监视与 [池跟踪](pool-tracking.md) 选项相关的统计信息。 如果此选项不处于活动状态，则它们均为零。

这些统计信息分为两部分： **分页池** 和 **非分页池**。 对于每种类型的内存池，将显示以下四个计数器：

<span id="Current_Number_of_Allocations"></span><span id="current_number_of_allocations"></span><span id="CURRENT_NUMBER_OF_ALLOCATIONS"></span>**当前分配数**  
指定的驱动程序从此类型的内存池中进行的单个分配的当前数目。

<span id="Peak_Number_of_Allocations"></span><span id="peak_number_of_allocations"></span><span id="PEAK_NUMBER_OF_ALLOCATIONS"></span>**最大分配数**  
自上一次启动之后由指定的驱动程序从此类型的内存池中进行的单个分配的最大数目。

<span id="Current_Bytes_Allocated"></span><span id="current_bytes_allocated"></span><span id="CURRENT_BYTES_ALLOCATED"></span>**当前分配的字节数**  
从此类型的内存池中分配给指定驱动程序的当前字节数。

<span id="Peak_Bytes_Allocated"></span><span id="peak_bytes_allocated"></span><span id="PEAK_BYTES_ALLOCATED"></span>**已分配的峰值字节**  
自上一次启动到指定驱动程序之后，在此类型的内存池中任意一次分配的最大字节数。

大小为一页或更大的分配不会被池跟踪跟踪，无法从特殊池进行分配。 这些单个计数器不反映这些大型分配。 可以在 [全局计数器](monitoring-global-counters.md)中查看所有此类分配的计数。

 

 





