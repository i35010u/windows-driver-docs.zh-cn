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
ms.openlocfilehash: 053e26b6b69656a7f4141045dda46e920d94e8f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840294"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件编译和生成环境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


使用 Windows 驱动程序工具包（WDK）8时，可以通过选择 "发布（免费）" 或 "调试（已检查）" 配置，有条件地编译您的驱动程序中的调试代码。 您选择的配置设置**DBG**预处理器常数。

**DBG**的值取决于你选择用于构建驱动程序的生成配置：

-   如果使用调试（已选中）配置创建驱动程序， **DBG**将等于1。

-   如果使用 release （免费）生成配置创建驱动程序，则**DBG**将等于0（如果不包括 wdm 和 ntddk，则不会定义）。

调试例程[**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))、 [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)、 [**KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))、 [**KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus)、 [**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)和[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)实际上是根据**DBG**的值有条件地定义的宏。 如果为0，则这些宏为非 ops。 因此，这些宏仅在驱动程序的调试（已检查）版本中处于活动状态。

**请注意**   以字母 "Kd" 开头的所有调试例程在驱动程序的自由版本中不起作用， **KdRefreshDebuggerNotPresent**除外。

 

有关使用 Visual Studio 和 MSBuild 创建以发布和调试驱动程序版本的详细信息，请参阅[构建驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)和[WDK 和 Visual Studio 生成环境](wdk-and-visual-studio-build-environment.md)。

 

 





