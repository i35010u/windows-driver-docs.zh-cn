---
title: 测试驱动程序代码和驱动程序包的相关建议。
description: 应在何时开始测试？ 了解驱动程序的要求后，便可以立即开始设计测试用例来测试是否已实现了这些关键要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae1fc357a6d5556948e9a368bef5bf3597de9c22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784125"
---
# <a name="tips-for-testing-drivers-during-development"></a>开发期间测试驱动程序的相关技巧

**应在何时开始测试？** 了解驱动程序的要求后，便可以立即开始设计测试用例来测试是否已实现了这些关键要求。 研究表明，缺陷在代码中存在得越久，找到并修复这些缺陷就变得越代价高昂。 在开发周期的早期找到并修复缺陷，比在代码发布和分发之后查找缺陷成本更低、中断更少。 尽早创建测试用例还可以帮助你找出设计中存在的问题。

## <a name="span-idsuggestions_for_testing_driversspanspan-idsuggestions_for_testing_driversspansuggestions-for-testing-during-development"></a><span id="suggestions_for_testing_drivers"></span><span id="SUGGESTIONS_FOR_TESTING_DRIVERS"></span>开发期间的测试建议


按照以下建议来测试驱动程序代码和驱动程序包。

**如何帮助你在编译时找到 Bug：**

-   使用函数角色类型声明驱动程序提供的回调函数和调度例程。 这有助于提高代码分析和验证工具的准确性以及测试时间的有效性。 有关如何声明驱动程序提供的函数的详细信息，请参阅[使用函数角色类型声明](../devtest/using-function-role-type-declarations.md)。

-   使用“**Level4 (/W4)** 警告”选项编译代码。 解决编译器检测到的警告问题将提高驱动程序代码的质量，并帮助在开发周期内更早地消除其他缺陷。
-   使用 Microsoft 源代码注释语言 (SAL) 2.0 为代码添加注释。 注释描述函数如何使用其参数 - 函数针对参数作出的假设，及其在完成后所做的保证。 注释还提高了代码分析工具的准确性。 有关驱动程序特定注释的详细信息，请参阅[驱动程序的 SAL 2.0 注释](../devtest/sal-2-annotations-for-windows-drivers.md)。
-   在开发驱动程序时使用[用于验证驱动程序的工具](../devtest/tools-for-verifying-drivers.md)。 有关何时使用特定验证工具的指南，请参阅[使用代码分析和验证工具分析驱动程序](analyzing-driver-quality-by-using-code-analysis-tools.md)和[验证工具调查](../devtest/survey-of-verification-tools.md)。

**如何测试驱动程序包：**

-   在开发过程的早期创建 INF 文件和驱动程序包，并在整个测试中使用。

-   使用 [InfVerif](../devtest/infverif.md) 工具来验证 INF 文件的结构和语法，并帮助你诊断 INF 文件和其他安装相关问题。

-   使用 [**Inf2Cat**](../devtest/inf2cat.md) 工具（通过 **/nocat** 选项）来执行额外的 INF 文件验证。 **Inf2Cat** 可以验证 INF 引用的文件是否存在并放在 INF 预期的包目录中。

-   签署驱动程序可以推进驱动程序的安装和测试，如[在开发和测试期间签署驱动程序](../install/introduction-to-test-signing.md)中所述。

-   运行作为 WDK 中提供的设备基础功能测试的一部分包含的 **DriverInstall** 测试。 请参阅[如何使用 Visual Studio 在运行时测试驱动程序](testing-a-driver-at-runtime.md)和[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)。 **DriverInstall** 测试可以在驱动程序部署到测试计算机后运行。 可以将 **DriverInstall** 测试添加到驱动程序测试组。 **DriverInstall** 测试显示在 All Tests\\Basic\\Device Fundamentals\\DriverInstall 下的 **驱动程序测试类别** 中。

-   通过使用设备管理器查看有关驱动程序和设备的系统信息并通过参考 SetupAPI 日志来[解决设备安装](../install/troubleshooting-device-and-driver-installations.md)问题。 SetupAPI 日志包含设备或驱动程序安装期间所发生的操作序列的相关信息。

    使用 Visual Studio 和 WDK，将驱动程序部署到测试计算机时，可以测试驱动程序包的安装并解决相关问题，请参阅[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)。 从[驱动程序包项目的部署属性](deployment-properties-for-driver-projects.md)中选择“安装并验证”  选项。 如果你选择此选项，并指定“默认驱动程序包安装任务(可能重新启动)”  或“默认打印机驱动程序包安装任务(可能重新启动)”  ，则测试将读取驱动程序的 INF 文件并安装驱动程序。 然后，测试将验证该驱动程序是否已启动且正在运行。 完成后，测试将提供有关安装任务成功与否的详细信息。 结果显示在 **驱动程序测试组资源管理器** 中的“驱动程序测试组”&gt;“驱动程序安装”下。 任务名称为“默认驱动程序包安装任务”  。

**如何在运行时测试驱动程序：**

-   运行 WDK 中包括的设备基础功能测试。 请参阅[如何使用 Visual Studio 在运行时测试驱动程序](testing-a-driver-at-runtime.md)和[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)。

-   设置调试程序，以便可以排查和调试测试结果显示的问题。 有关详细信息，请参阅 [Windows 调试入门](../debugger/getting-started-with-windows-debugging.md)。
 
-   在用于部署的测试计算机上启用驱动程序验证程序，请参阅[驱动程序项目的驱动程序验证程序属性](driver-verifier-properties-for--driver-projects.md)。 选择 [DDI 符合性检查](../devtest/ddi-compliance-checking.md)选项。 如果你的驱动程序未通过 DDI 符合性检查，请运行[静态驱动程序验证程序](../devtest/static-driver-verifier.md)，并指定导致失败的规则。 静态驱动程序验证程序可以帮助你找到源文件中存在的 Bug 的原因。
-   在尽可能多的不同硬件配置上测试你的驱动程序和设备。 改变硬件可以帮助你找到设备交互中出现的设备错误与其他错误之间的冲突。 例如，你应该在具有不同处理器体系结构的计算机以及运行 32 位和 64 位 Windows 版本的计算机上测试驱动程序和设备。

-   在多处理器系统上测试驱动程序和设备。 以其他方式无法找到的争用条件及其他计时问题会出现在多处理器系统中。 请参阅[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)和[用于测试驱动程序的多处理器组支持的启动参数](../devtest/boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

-   测试驱动程序的特定系统和硬件条件，特别是边界条件。 例如，这些条件可能包括“D3 hot”和“D3 cold”。 确保你的驱动程序和设备可以从设备电源状态“D3 hot”（不消耗功率）和“D3 cold”（从设备中移除电源时）正确返回。 有关详细信息，请参阅[如何选择和配置设备基础功能测试](how-to-select-and-configure-the-device-fundamental-tests.md)。
