---
title: 条件编译和生成环境
description: 条件编译和生成环境
ms.assetid: 7879b6c6-4985-4817-a8bc-b287397df721
keywords:
- DBG 预处理器常量
- 调试代码 WDK、 条件编译
- 调试代码 WDK 构建环境
- 条件编译 WDK 调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6550d4411052d1a90e7dd87871f245f46976ad4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371586"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件编译和生成环境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


当使用 Windows Driver Kit (WDK) 8 可以有条件地编译方法是选择 （免费） 的版本或调试 （已选中） 配置您的驱动程序中的调试代码。 选择集的配置**DBG**预处理器常量。

值**DBG**取决于你选择生成您的驱动程序的生成配置：

-   如果创建使用调试 （已选中） 配置，您的驱动程序**DBG**将等于 1。

-   如果使用发行版 （免费） 的生成配置，创建您的驱动程序**DBG**将等于 0 （或如果包括 wdm.h 中既不 ntddk.h 则是未定义）。

调试例程[ **ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))， [ **ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-assertmsg)， [ **KdBreakPoint**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548063(v=vs.85))， [ **KdBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdbreakpointwithstatus)， [ **KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprint)，并[ **KdPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprintex)是实际有条件地根据的值定义的宏**DBG**。 如果该值为 0，这些宏不会进行任何操作。 因此，这些宏处于活动状态只在一个驱动程序 （已选中） 的调试版本中。

**请注意**   "Kd"的字母开头的所有调试例程不起作用的驱动程序，免费版本中除**KdRefreshDebuggerNotPresent**。

 

有关使用 Visual Studio 和 MSBuild 创建发布和调试版本的驱动程序的详细信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)并[WDK 和 Visual Studio 构建环境](wdk-and-visual-studio-build-environment.md)。

 

 





