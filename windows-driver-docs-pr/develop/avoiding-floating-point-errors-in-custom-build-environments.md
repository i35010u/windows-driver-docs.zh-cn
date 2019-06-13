---
ms.assetid: 47AC8BD7-7098-43C3-A198-3622D465B142
title: 避免自定义生成环境内出现浮点错误
description: 此信息主要面向开发人员和为 Windows 编译内核模式驱动程序的构建工程师。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c2f017367c211eb8020ea8ee3f29d29509467ee
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63359485"
---
# <a name="avoiding-floating-point-errors-in-custom-build-environments"></a>避免自定义生成环境内出现浮点错误

此信息主要面向开发人员和为 Windows 编译内核模式驱动程序的构建工程师。 在 Microsoft Visual Studio Professional 2012 中，Visual C++ (VC++) 编译器的默认体系结构从 IA32 更改为流式 SIMD 扩展 2 (SSE2) 指令集。 如果未考虑这一点，由于此更改，编译时注入二进制文件的 SSE2 浮点 (FP) 指令可能会产生浮点错误。 使用 Microsoft VC++ 编译器，或自定义生成环境开发 Windows 驱动程序的人员可能会遇到此问题。 但此问题不会影响借助 Microsoft Visual Studio 开发环境或 MSbuild 实用工具，利用未修改的工具集生成驱动程序的开发人员。

## <a name="span-idfloatingpointerrorscancausedatacorruptionorcomputercrashesspanspan-idfloatingpointerrorscancausedatacorruptionorcomputercrashesspanspan-idfloatingpointerrorscancausedatacorruptionorcomputercrashesspanfloating-point-errors-can-cause-data-corruption-or-computer-crashes"></a><span id="Floating_point_errors_can_cause_data_corruption_or_computer_crashes_"></span><span id="floating_point_errors_can_cause_data_corruption_or_computer_crashes_"></span><span id="FLOATING_POINT_ERRORS_CAN_CAUSE_DATA_CORRUPTION_OR_COMPUTER_CRASHES_"></span>浮点错误可能导致数据损坏或计算机故障


如果不  使用 WDK、Visual Studio 和为 Windows 驱动程序 (**WindowsKernelModeDriver8.0**) 推荐的平台工具集编译驱动程序，驱动程序可能无法正确管理浮点操作，即使驱动程序能够正确编译也是如此。

Visual Studio Professional 2012 VC++ 编译器通过设置 **/arch:sse2** 编译器选项发出使用 SSE2 指令集的代码。 从 Visual Studio Professional 2012 开始，这成为 x86 VC++ 编译器代码生成的默认选项。 具体来说，是默认值从 **/arch:ia32** 更改为 **/arch:sse2**。

对于应用程序，此更改将生成能够在执行期间表现更佳且使用更少处理器时间的代码。 但是，对于内核模式驱动程序，此更改将无法正确管理浮点 (FP) 状态。 这是由于 VC++ 编译器在未保存上下文的位置引入了 FP 指令序列。 任何二进制浮点系统都只能准确地表示有限数量的浮点值，其余为近似值。 浮点控制状态（如舍入模式或精度）可令 FP 操作保持相互同步。 未定义状态时，这将导致 FP 计算错误。 这些计算错误很难检测，因为在大多数情况下，应用程序状态异常是此问题的唯一征兆。 这种异常可能有多种表现，从无规律崩溃到数据损坏都有可能。

## <a name="span-idsolutionspanspan-idsolutionspanspan-idsolutionspansolution"></a><span id="Solution"></span><span id="solution"></span><span id="SOLUTION"></span>解决方案


若要避免浮点计算出现这些问题，请将 **/kernel** 标志添加到 C++ 编译器和链接器命令行以防止生成 SSE2 指令。 **/kernel** 标志将默认的 **/arch:sse2** 值重新更改为 **/arch:ia32**。

此外，如果你使用 WDK 和 Visual Studio Professional 2012 开发环境，或在“Visual Studio 命令提示”窗口使用 MSBuild 生成驱动程序，Microsoft 提供的平台工具集 (**WindowsKernelModeDriver8.0**) 将设置 **/kernel** 标志。 这样就可以避免浮点生成错误。

```cpp
msbuild myProject.vcxproj /p:PlatformToolset=WindowsKernelModeDriver8.0
```

## <a name="span-idrecommendationsspanspan-idrecommendationsspanspan-idrecommendationsspanrecommendations"></a><span id="Recommendations"></span><span id="recommendations"></span><span id="RECOMMENDATIONS"></span>建议


下面是根据你使用的开发环境类型建议的解决方案：

-   **Microsoft 工具集 (MSBuild)** - 无需操作。 使用 **WindowsKernelModeDriver8.0** 作为平台工具集， **/kernel** 将在适当时自动添加。
-   **Microsoft VC++ 编译器** - 添加 **/kernel** 标志以防止编译器发出 SSE2。
-   **自定义工具/非 Microsoft 编译器** - 必须手动设置生成的二进制文件中使用的程序集指令。

 

 





