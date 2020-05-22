---
title: 面向 WDK 开发人员的 MSBuild 入门教程
description: 本部分介绍了一些基本的 MSBuild 术语，适用于 WDK 开发人员，熟悉 al.exe 和 NMake。 本部分展示了简单的 MSBuild 项目的构造。
ms.assetid: EA223DF3-71FF-442F-B3E8-56C3B57F7B67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78d1693eb029ff6640a5f84110a37facc68b37d1
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769629"
---
# <a name="msbuild-primer-for-wdk-developers"></a>面向 WDK 开发人员的 MSBuild 入门教程


本部分介绍了一些基本的 MSBuild 术语，适用于 WDK 开发人员，熟悉 al.exe 和 NMake。 本部分展示了简单的 MSBuild 项目的构造。

## <a name="span-idnmake_concepts_relevant_to_msbuildspanspan-idnmake_concepts_relevant_to_msbuildspanspan-idnmake_concepts_relevant_to_msbuildspannmake-concepts-relevant-to-msbuild"></a><span id="Nmake_concepts_relevant_to_MSBuild"></span><span id="nmake_concepts_relevant_to_msbuild"></span><span id="NMAKE_CONCEPTS_RELEVANT_TO_MSBUILD"></span>与 MSBuild 相关的 Nmake 概念


如果你使用的是 WDK 和以前版本的 WDK （WDK 8 之前的版本），则可能会熟悉 NMake 使用的术语和概念。

-   **命令**-调用命令行工具。
-   **target** -描述指定的命令序列。
-   **依赖关系**-描述依赖于其他目标的目标。
-   在指定了一个或多个目标的 make 文件上调用 Nmake。 然后，它会以递归方式运行所有依赖项，然后运行目标的命令。
-   Nmake 文件可包含其他生成文件以实现生成结构的强大管理。
-   Nmake 还支持创建将替换为命令参数的命名变量。
-   Nmake 还支持由 Make 本身分配的自动变量，例如，当前目录或路径的名称。
-   在单个生成过程中，目标永远不会运行两次。 运行后，假定目标已完成其工作，并且不会再次运行，即使生成中的后续目标依赖于该目标。

## <a name="span-idmsbuild_concepts_spanspan-idmsbuild_concepts_spanspan-idmsbuild_concepts_spanmsbuild-concepts"></a><span id="MSBuild_concepts_"></span><span id="msbuild_concepts_"></span><span id="MSBUILD_CONCEPTS_"></span>MSBuild 概念


-   C + + 项目的主 MSBuild 文件扩展名为 .vcxproj。
-   命令现在称为*任务*，它们不只是调用命令行进程。 相反，任务是 MSBuild 可用于执行原子生成操作的可执行代码单元。 有关任务的完整列表，请参阅[特定于 Visual C++ 的 MSBuild 任务](https://docs.microsoft.com/visualstudio/msbuild/msbuild-tasks-specific-to-visual-cpp)。
-   MSBuild 从其公共语言运行时（CLR）程序集导入任务，如下面的**示例所示**。
    ```
    <UsingTask TaskName="TaskName" AssemblyName="AssemblyName" />
    ```

-   目标按特定的顺序将任务组合在一起，并允许生成过程分为较小的单位。
-   **PropertyGroup**允许使用友好格式定义属性。 下面的示例显示**PropertyGroup**格式。
    ```
    <PropertyGroup>
      <ProductVersion>9.0.30729</ProductVersion>
    </PropertyGroup>
    ```

-   **项**是面向对象的**属性**的变量。 如果属性格式为名称/值，则项格式为名称/对象，其中对象具有多个属性。 **项**是对象的数组。
-   用 **@ （name）** 格式引用项时，将用 **$ （project）** 格式引用**属性**。
-   **ItemGroup**是项的集合 **。**
-   通常， **ItemGroups**是要编译的所有文件的列表。 然后，使用 **@ （** 文件 _）表示法将文件集合传递给任务。 有关使用项的详细信息，请参阅[MSBuild 项](https://docs.microsoft.com/visualstudio/msbuild/msbuild-items) **。**
-   MSBuild 具有许多[内置属性](https://docs.microsoft.com/visualstudio/msbuild/msbuild-reserved-and-well-known-properties)，您还可以在项目文件中引用这些属性。
-   有关 MSBuild 和生成任务的详细信息，请参阅[Msbuild 概念](https://docs.microsoft.com/visualstudio/msbuild/msbuild-concepts)和[msbuild 参考](https://docs.microsoft.com/visualstudio/msbuild/msbuild-reference)。

 

 





