---
title: 将 WDK 源文件转换为 Visual Studio 项目
description: 使用 Nmake2msBuild 将 WDK 源文件转换为 Visual Studio 项目。
ms.assetid: 6030317B-5068-40FD-8C9A-0B7A48C82B31
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ada247897777a06a5a1d083a1fb8c4fcff768391
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360375"
---
# <a name="converting-a-wdk-sources-file-to-a-visual-studio-project"></a>将 WDK 源文件转换为 Visual Studio 项目


**请注意**Nmake2MsBuild 工具已从 WDK 从 Windows 10，版本 1511年开始。

 

对于 Windows 7 WDK 的大多数项目，使用 Build.exe 生成，你可以使用[Nmake2MsBuild](nmake2msbuild.md)实用程序或 Visual Studio 中，以生成项目文件中的自动转换过程 (。VcxProj)。 在大多数情况下，Visual Studio 项目文件都紧密映射到原始*源*文件，以便在 Visual Studio 中，或从 MSBuild 的命令可以成功生成项目。 适用于某些生成目标，你需要自定义的转换工具使用的基于规则的映射。 本主题介绍转换实用程序的工作原理以及如何通过创建自己的规则映射扩展它。

## <a name="span-idthenmake2msbuildconversionprocessspanspan-idthenmake2msbuildconversionprocessspanspan-idthenmake2msbuildconversionprocessspanthe-nmake2msbuild-conversion-process"></a><span id="The_Nmake2MsBuild_conversion_process"></span><span id="the_nmake2msbuild_conversion_process"></span><span id="THE_NMAKE2MSBUILD_CONVERSION_PROCESS"></span>Nmake2MsBuild 转换过程


[Nmake2MsBuild](nmake2msbuild.md)工具将执行基于规则的内容的映射*源*文件内容的 Visual StudioC++项目文件 (。VcxProj)。 对于要转换每个生成宏，没有相应的转换规则中使用 msbuild 和生成期间检测到的属性文件 (.props)。 在 MSBuild 环境中，属性、 项和对这些项的元数据的生成系统使用。 在每个宏*源*文件映射到 MSBuild 属性、 项或作为由规则指定项元数据。 默认情况下，如果没有规则存在，则宏名为 A，B 的值转换为属性的值 b。初始转换步骤涉及 NMake 语法中的映射*makefile.inc*或*源*MSBuild 语法关联的属性文件 (.props) 中的文件。 NMake 文件中的每个宏转换为属性文件 (.props) 中的属性。 在生成期间，这些属性的计算，并已某些属性的计算的值进行映射到各种属性、 项或作为指定的转换规则元数据。

例如，用户\_C\_中的标志宏*源*文件用于指定在生成过程传递到编译器 (cl.exe) 的命令行参数。 在 MSBuild 环境中，ClCompile 项目列表包含将编译的源代码文件。 ClCompile 项列表由在编译器[CL 任务](https://docs.microsoft.com/visualstudio/msbuild/cl-task?view=vs-2015)。 在列表中的每个项上的其他元数据确定其他标志传递到编译器 (cl.exe)。 因此，用户的值\_C\_标志宏应映射到类型 ClCompile 的项的其他项元数据。 在初始转换步骤中，用户\_C\_源文件中的标志宏转换为 MSBuild 属性，也称为用户\_C\_标志生成的文件中名为*sources.props*. 用户的计算值的映射\_C\_在生成时，发生的其他元数据的标志属性，如下面的示例中所示：

```
  <!-- Contains rules to map compiler and linker switches -->
  <ItemDefinitionGroup>
    <ClCompile>
      ...
      <AdditionalOptions>%(AdditionalOptions) $(User_C_Flags)</AdditonalOptions>
      ...
    </ClCompile>
  </ItemDefinitionGroup>
```

在前面的示例所示的映射是从 PostToolsetRules.props 文件。 示例映射使用 MSBuild ItemDefinitionGroup 来指定 $(用户\_C\_标志) 应追加到类型 ClCompile AdditonalOptions 元数据中的所有项。 您可以查找的属性在 c： 驱动器中转换过程中使用的文件\\Program Files (x86)\\Windows 工具包\\8.0\\bin\\转换目录。

所有的转换规则是使用标准 MSBuild 语法进行指定。

## <a name="span-iddefaultconversionrulesfilespanspan-iddefaultconversionrulesfilespanspan-iddefaultconversionrulesfilespandefault-conversion-rules-file"></a><span id="Default_conversion_rules_file"></span><span id="default_conversion_rules_file"></span><span id="DEFAULT_CONVERSION_RULES_FILE"></span>默认的转换规则文件


PostToolsetRules.props 文件中指定用于转换的默认规则。 您可以找到 PostToolsetRules.props 文件和其他转换属性文件 c:\\Program Files (x86)\\Windows 工具包\\8.0\\bin\\转换目录。 用于创建你的项目转换为的新规则，可以作为参考使用 PostToolsetRules.props 文件。

## <a name="span-idcreatingcustomconversionrulesspanspan-idcreatingcustomconversionrulesspanspan-idcreatingcustomconversionrulesspancreating-custom-conversion-rules"></a><span id="Creating_custom_conversion_rules"></span><span id="creating_custom_conversion_rules"></span><span id="CREATING_CUSTOM_CONVERSION_RULES"></span>创建自定义转换规则


在转换期间，始终使用默认规则文件，PostToolsetRules.props，但您还可以创建自己的自定义规则文件。 自定义规则文件可能是特定于在其下之前生成项目的生成环境的任何生成宏提供了附加的转换规则。

由 Microsoft 提供的规则仅支持转换使用的宏和 Windows 7 WDK 中定义的目标的项目。 例如，规则仅支持这些宏和中显示的目标*makefile.new*。 不保证的功能在以前的生成环境中添加或修改任何项目转换为自动。 作为一般规则转换规则文件时需要现有的项目未生成无需修改的源或与项目相关联的.inc 文件或安装 WDK 的任何其他文件的 Windows 7 wdk 的全新安装。

自定义规则文件应遵循标准的 MSBuild 语法，以及默认规则文件使用的设计模式。 默认规则应该用于开发所有提供足够的准则和示例，但最复杂的转换规则。

在其中导入文件中的顺序。VcxProj 文件和规则检测到，至关重要，因此应进行维护。 建议您导入项目的用户开发规则文件 Microsoft 提供的 PostToolsetRules.props 后立即：

```
  <Import Project="$(PostToolsetRules)" />
  <!-- Import PostToolsetRules to map nmake properties/macros to msbuild properties/items/metadata -->
```

## <a name="span-idconversiontoollimitationsspanspan-idconversiontoollimitationsspanspan-idconversiontoollimitationsspanconversion-tool-limitations"></a><span id="Conversion_tool_limitations"></span><span id="conversion_tool_limitations"></span><span id="CONVERSION_TOOL_LIMITATIONS"></span>转换工具限制


NMake2MsBuild 实用工具不支持的自定义目标的转换或某些非生成关键目标，例如 BinPlace 的转换。 BinPlace 本身支持 MSBuild.exe 环境中，但不是自动转换。 NMake2MsBuild 实用程序不提供 Visual Studio 属性页中查看已转换项目的所有设置的功能。

## <a name="span-idnmakesyntaxandbehaviornotsupportedbynmake2msbuildspanspan-idnmakesyntaxandbehaviornotsupportedbynmake2msbuildspanspan-idnmakesyntaxandbehaviornotsupportedbynmake2msbuildspannmake-syntax-and-behavior-not-supported-by-nmake2msbuild"></a><span id="NMake_syntax_and_behavior_not_supported_by_Nmake2Msbuild"></span><span id="nmake_syntax_and_behavior_not_supported_by_nmake2msbuild"></span><span id="NMAKE_SYNTAX_AND_BEHAVIOR_NOT_SUPPORTED_BY_NMAKE2MSBUILD"></span>NMake 语法和行为不受 Nmake2Msbuild


-   在定义可选的目录的推理规则中引用的宏扩展：

    ```
    INPUT_DIR= c:\MyDirectory
    .FromExt{$(INPUT_DIR)}.ToExt:
         cmd.exe /c echo  something 
    ```

    您 d 必须更改为更高版本：

    ```
    .FromExt{ c:\MyDirectory}.ToExt:
         cmd.exe /c echo  something 
    ```

-   不支持 NMAKE 内联文件和宏替换。

    NMAKE 内联文件：请参阅**创建内联文件文本**

    宏替换：请参阅**宏替换**

    因为不支持内联文件和宏替换正确转换结束-赢得 t 的以下目标：

    ```
    fsdkmsg.mc : ..\..\wrapper\fsdkmsgbase.src
           copy ..\..\wrapper\fsdkmsgbase.src
        @type <<$(ECHO_RSP)
    $(ECHO_MSG_P) /EP $**
    <<$(BUILD_NOKEEP)
        @$(C_PREPROCESSOR_NAME) @<<$(CL_RSP) /Tc$** > $@
    $(CPPXX: =
    )
    <<$(BUILD_NOKEEP)   
    ```

-   **!错误**语句将不会转换。 有 s 也以目标会起作用的外部 MSBuild 的 MSBuild 中没有等效项。
-   目标定义必须匹配 1 对 1 与 NTTARGETFILE\*调用目标的宏：不支持以下：

    ```
    Sources File:
    OBJ_NAME=Something
    NTTARGETFILES=$(_OBJ_DIR)\$(TARGET_DIRECTORY)\$(OBJ_NAME).obj
    Makefile.inc:
    obj\$(TARGET_DIRECTORY)\Something.obj : $(_OBJ_DIR)\$(TARGET_DIRECTORY)\$(Foo).obj
      
    ```

-   必须匹配的目标的定义和 NTTARGETFILES;它们都应使用 $(OBJ\_NAME).obj 或*Somename*。 目标 $？ 和 $&lt;目标中的令牌总是扩展为所有依赖项。

    请参阅**文件名宏**有关详细信息。

-   $? 将扩展到更高版本的时间戳比当前的目标的所有依赖项。  转换项目忽略时间戳，并且此计算结果为所有依赖项。 如此&lt;

## <a name="span-idlimitationsofconvertedprojectsspanspan-idlimitationsofconvertedprojectsspanspan-idlimitationsofconvertedprojectsspanlimitations-of-converted-projects"></a><span id="Limitations_of_Converted_Projects"></span><span id="limitations_of_converted_projects"></span><span id="LIMITATIONS_OF_CONVERTED_PROJECTS"></span>转换项目的限制


如果原始的源文件进行条件编译一组不同的文件和修改已转换的项目，方法是在 IDE 中重命名/删除/添加文件，然后将仅在更新的文件列表上运行项目。 它将不再有条件地编译不同的文件。

转换后的项目不支持 VS。筛选文件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Nmake2MsBuild](nmake2msbuild.md)

[从现有源文件创建驱动程序](https://docs.microsoft.com/windows-hardware/drivers)

 

 






