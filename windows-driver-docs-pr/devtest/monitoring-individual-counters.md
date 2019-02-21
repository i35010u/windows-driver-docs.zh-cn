---
title: 监视单个计数器
description: 监视单个计数器
ms.assetid: 95d4492b-20b9-401a-97aa-eaf700b64420
keywords:
- 各个计数器 WDK Driver Verifier
- 驱动程序验证程序 WDK 计数器
- WDK 驱动程序验证程序的统计信息
- 计数器 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38eca341c7ad8773b27f16f5886e018e3b9c8b19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534551"
---
# <a name="monitoring-individual-counters"></a>监视单个计数器


## <span id="ddk_monitoring_individual_counters_tools"></span><span id="DDK_MONITORING_INDIVIDUAL_COUNTERS_TOOLS"></span>


*各个计数器*会监视某些驱动程序验证程序的驱动程序执行的操作的统计信息。 正在验证每个驱动程序的单独保留这些统计信息。

可以通过查看各个计数器[**验证程序命令行**](verifier-command-line.md)，或通过使用驱动程序验证程序管理器。 有两个版本的驱动程序验证程序管理器-一个用于[Windows 2000](driver-verifier-manager--windows-2000-.md) ，另一个用于[Windows XP 及更高版本](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>验证程序命令行

若要查看各个计数器，请使用**verifier /query**命令。 这将显示两个单独的计数器和[全局计数器](monitoring-global-counters.md)。

各个计数器也包括在 Driver Verifier[日志文件](creating-log-files.md)。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>驱动程序验证程序管理器 (Windows 2000)

若要查看各个计数器，请选择**池跟踪**选项卡。然后从下拉列表框中选择所需的驱动程序。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>驱动程序验证程序管理器 (Windows XP 及更高版本)

若要查看各个计数器，请启动驱动程序验证程序管理器，并选择**显示有关当前已验证的驱动程序信息**任务。 然后按**下一步**三次。

最后，从下拉列表框中选择所需的驱动程序。

### <a name="span-idexplanationofindividualcountersspanspan-idexplanationofindividualcountersspanexplanation-of-individual-counters"></a><span id="explanation_of_individual_counters"></span><span id="EXPLANATION_OF_INDIVIDUAL_COUNTERS"></span>单个计数器的说明

各个计数器监视到相关的统计信息[池跟踪](pool-tracking.md)选项。 它们将全部为零如果此选项处于非活动状态。

这些统计信息可分为两个部分：**页面缓冲池**并**非分页缓冲的池**。 对于每个类型的内存池，显示以下四个计数器：

<span id="Current_Number_of_Allocations"></span><span id="current_number_of_allocations"></span><span id="CURRENT_NUMBER_OF_ALLOCATIONS"></span>**当前的分配数**  
当前的单个所分配的对象指定的驱动程序从该类型的内存池数。

<span id="Peak_Number_of_Allocations"></span><span id="peak_number_of_allocations"></span><span id="PEAK_NUMBER_OF_ALLOCATIONS"></span>**分配的最大资源数**  
单个执行的分配在上一次启动的任何单个时间由指定的驱动程序从该类型的内存池最大数量。

<span id="Current_Bytes_Allocated"></span><span id="current_bytes_allocated"></span><span id="CURRENT_BYTES_ALLOCATED"></span>**当前分配的字节数**  
当前分配给指定的驱动程序从该类型的内存池的字节数。

<span id="Peak_Bytes_Allocated"></span><span id="peak_bytes_allocated"></span><span id="PEAK_BYTES_ALLOCATED"></span>**分配的峰值字节数**  
最大在上一次启动的任何单个时间从分配给指定的驱动程序内存池的此类型的字节数。

其大小不是一个页面或更大的分配池跟踪由跟踪，并且不能从特殊池分配。 这些单独的计数器不反映这些大的分配。 所示的所有此类分配计数[全局计数器](monitoring-global-counters.md)。

 

 





