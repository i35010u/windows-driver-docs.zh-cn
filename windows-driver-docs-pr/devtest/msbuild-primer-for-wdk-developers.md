---
title: MSBuild WDK 开发人员的入门读物
description: 本部分介绍到 WDK 开发人员，他们熟悉 Build.exe 和 NMake.exe 的一些基本的 MSBuild 术语。 本部分显示了简单的 MSBuild 项目中的构造。
ms.assetid: EA223DF3-71FF-442F-B3E8-56C3B57F7B67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4745f3c158ecc2732ce373e305795edc9ca9178
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542492"
---
# <a name="msbuild-primer-for-wdk-developers"></a>MSBuild WDK 开发人员的入门读物


本部分介绍到 WDK 开发人员，他们熟悉 Build.exe 和 NMake.exe 的一些基本的 MSBuild 术语。 本部分显示了简单的 MSBuild 项目中的构造。

## <a name="span-idnmakeconceptsrelevanttomsbuildspanspan-idnmakeconceptsrelevanttomsbuildspanspan-idnmakeconceptsrelevanttomsbuildspannmake-concepts-relevant-to-msbuild"></a><span id="Nmake_concepts_relevant_to_MSBuild"></span><span id="nmake_concepts_relevant_to_msbuild"></span><span id="NMAKE_CONCEPTS_RELEVANT_TO_MSBUILD"></span>Nmake 概念相关的 msbuild


如果您曾经使用 Build.exe 及早期版本的 WDK （之前 WDK 8)，您都可能已经熟悉的术语和概念 NMake.exe 使用。

-   **命令**-调用命令行工具。
-   **目标**-介绍命令的已命名的序列。
-   **依赖项**-介绍了依赖于其他目标的目标。
-   Nmake 调用上生成具有指定的一个或多个目标文件。 然后运行所有依赖项以递归方式，然后目标的命令。
-   Nmake 文件可以包括其他使文件来生成结构的强大的管理。
-   Nmake 还支持创建命名的变量，将替换参数的命令。
-   Nmake 还支持自动分配 Make.exe 本身，例如，路径的当前目录的名称的变量。
-   目标将永远不会运行一次生成过程中两次。 运行后，目标被认为已完成其工作，不会再次运行，即使在生成中的后续目标依赖于它。

## <a name="span-idmsbuildconceptsspanspan-idmsbuildconceptsspanspan-idmsbuildconceptsspanmsbuild-concepts"></a><span id="MSBuild_concepts_"></span><span id="msbuild_concepts_"></span><span id="MSBUILD_CONCEPTS_"></span>MSBuild 概念


-   C + + 项目主要的 MSBuild 文件扩展名为.vcxproj。
-   现在调用命令*任务*，它们也不是只需调用的命令行进程。 相反，任务是可执行代码单元，可以使用 MSBuild 来执行原子生成操作。 有关任务的完整列表，请参阅[特定于 Visual c + + 的任务 MSBuild]( https://go.microsoft.com/fwlink/p/?linkid=236121)...
-   MSBuild 将任务从其公共语言运行时 (CLR) 程序集与导入**UsingTask**元素，如以下示例所示。
    ```
    <UsingTask TaskName="TaskName" AssemblyName="AssemblyName" />
    ```

-   目标按特定顺序将任务组合到一起，并允许生成过程以划分成更小的单位。
-   一个**PropertyGroup**允许使用用户友好格式定义的属性。 下面的示例演示**PropertyGroup**格式。
    ```
    <PropertyGroup>
      <ProductVersion>9.0.30729</ProductVersion>
    </PropertyGroup>
    ```

-   **项**是面向对象的变体**属性**。 名称/值的属性格式时，项格式将为名称/对象其中对象具有多个属性。 **项**是对象的数组。
-   **属性**格式引用 **$ （project)** 项引用格式时 **@(name)**。
-   **ItemGroup**是一系列**项。**
-   **ItemGroups**通常是列表的所有文件的编译。 然后，文件的集合传递给任务使用 **@(itemname)** 表示法。 请参阅[MSBuild 项](https://go.microsoft.com/fwlink/p/?linkid=236146)详细了解使用**项。**
-   MSBuild 拥有大量[内置属性](https://go.microsoft.com/fwlink/p/?linkid=236149)，你还可以引用项目文件中。
-   有关 MSBuild 和生成任务的详细信息，请参阅[MSBuild 概念](https://go.microsoft.com/fwlink/p/?linkid=236157)并[MSBuild 参考](https://go.microsoft.com/fwlink/p/?linkid=236161)。

 

 





