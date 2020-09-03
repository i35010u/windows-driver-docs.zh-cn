---
title: 条件编译和生成环境
description: 条件编译和生成环境
ms.assetid: 7879b6c6-4985-4817-a8bc-b287397df721
keywords:
- DBG 预处理器常量
- 调试代码 WDK，条件编译
- 调试代码 WDK，生成环境
- 条件编译 WDK 调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0276416f8c0c644c626213cb865d1698284bc47
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383999"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件编译和生成环境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


当你使用 Windows 驱动程序工具包 (WDK) 8 时，你可以通过选择 "释放" ("免费) " 或 "调试 (") 配置，有条件地编译驱动程序中的调试代码。 您选择的配置设置 **DBG** 预处理器常数。

**DBG**的值取决于你选择用于构建驱动程序的生成配置：

-   如果使用调试 (创建驱动程序) 配置，则 **DBG** 将等于1。

-   如果使用 release (免费) 生成配置来创建驱动程序，则 **DBG** 将等于 0 (; 如果不) 包括 wdm 和 ntddk，则不确定。

调试例程 [**ASSERT**](/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))、 [**ASSERTMSG**](/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)、 [**KdBreakPoint**](/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))、 [**KdBreakPointWithStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)、 [**KdPrint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)和 [**KdPrintEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex) 实际上是根据 **DBG**的值有条件地定义的宏。 如果为0，则这些宏为非 ops。 因此，这些宏仅在调试 (检查) 版本的驱动程序时才处于活动状态。

**注意**   所有以字母 "Kd" 开头的调试例程在驱动程序的自由版本中不起作用， **KdRefreshDebuggerNotPresent**除外。

 

有关使用 Visual Studio 和 MSBuild 创建以发布和调试驱动程序版本的详细信息，请参阅 [构建驱动程序](../develop/building-a-driver.md) 和 [WDK 和 Visual Studio 生成环境](wdk-and-visual-studio-build-environment.md)。

 

