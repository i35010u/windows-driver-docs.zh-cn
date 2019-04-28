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
ms.openlocfilehash: 01d7fddd58f0f6660af7e8ef44960367963ce962
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343095"
---
# <a name="conditional-compilation-and-the-build-environment"></a>条件编译和生成环境


## <span id="ddk_conditional_compilation_and_the_build_environment_tools"></span><span id="DDK_CONDITIONAL_COMPILATION_AND_THE_BUILD_ENVIRONMENT_TOOLS"></span>


当使用 Windows Driver Kit (WDK) 8 可以有条件地编译方法是选择 （免费） 的版本或调试 （已选中） 配置您的驱动程序中的调试代码。 选择集的配置**DBG**预处理器常量。

值**DBG**取决于你选择生成您的驱动程序的生成配置：

-   如果创建使用调试 （已选中） 配置，您的驱动程序**DBG**将等于 1。

-   如果使用发行版 （免费） 的生成配置，创建您的驱动程序**DBG**将等于 0 （或如果包括 wdm.h 中既不 ntddk.h 则是未定义）。

调试例程[ **ASSERT**](https://msdn.microsoft.com/library/windows/hardware/ff542107)， [ **ASSERTMSG**](https://msdn.microsoft.com/library/windows/hardware/ff542113)， [ **KdBreakPoint**](https://msdn.microsoft.com/library/windows/hardware/ff548063)， [ **KdBreakPointWithStatus**](https://msdn.microsoft.com/library/windows/hardware/ff548065)， [ **KdPrint**](https://msdn.microsoft.com/library/windows/hardware/ff548092)，并[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)是实际有条件地根据的值定义的宏**DBG**。 如果该值为 0，这些宏不会进行任何操作。 因此，这些宏处于活动状态只在一个驱动程序 （已选中） 的调试版本中。

**请注意**   "Kd"的字母开头的所有调试例程不起作用的驱动程序，免费版本中除**KdRefreshDebuggerNotPresent**。

 

有关使用 Visual Studio 和 MSBuild 创建发布和调试版本的驱动程序的详细信息，请参阅[构建一个驱动程序](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)并[WDK 和 Visual Studio 构建环境](wdk-and-visual-studio-build-environment.md)。

 

 





