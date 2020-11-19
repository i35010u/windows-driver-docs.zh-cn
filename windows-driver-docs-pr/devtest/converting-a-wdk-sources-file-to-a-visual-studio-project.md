---
title: 将 WDK 源文件转换为 Visual Studio 项目
description: 使用 Nmake2msBuild 将 WDK 源文件转换为 Visual Studio 项目。
ms.assetid: 6030317B-5068-40FD-8C9A-0B7A48C82B31
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 266648b845d8b4744c2ce2eb391e447b6277c76d
ms.sourcegitcommit: 878a1cb0149dc18ccbd31774e12bad76084dfa24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2020
ms.locfileid: "94937811"
---
# <a name="converting-a-wdk-sources-file-to-a-visual-studio-project"></a>将 WDK 源文件转换为 Visual Studio 项目


**注意**  从 Windows 10 1511 版开始，从 WDK 中删除了 Nmake2MsBuild 工具。

 

对于大多数使用 Build.exe 生成的 Windows 7 WDK 项目，你可以使用 [Nmake2MsBuild](nmake2msbuild.md) 实用工具或 Visual Studio 中的自动转换过程来 ( 生成项目文件。.Vcxproj) 。 在大多数情况下，Visual Studio 项目文件会密切映射 *到原始源文件* ，以便可以在 Visual Studio 中或通过 MSBuild 命令成功生成项目。 对于某些生成目标，需要自定义转换工具使用的基于规则的映射。 本主题介绍转换实用程序的工作原理，以及如何通过创建自己的规则映射来扩展它。

## <a name="span-idthe_nmake2msbuild_conversion_processspanspan-idthe_nmake2msbuild_conversion_processspanspan-idthe_nmake2msbuild_conversion_processspanthe-nmake2msbuild-conversion-process"></a><span id="The_Nmake2MsBuild_conversion_process"></span><span id="the_nmake2msbuild_conversion_process"></span><span id="THE_NMAKE2MSBUILD_CONVERSION_PROCESS"></span>Nmake2MsBuild 转换过程


[Nmake2MsBuild](nmake2msbuild.md)工具将 *从源* 文件的内容映射到 Visual Studio c + + 项目文件 ( 的内容。.Vcxproj) 。 对于要转换的每个生成宏，属性文件中都有相应的转换规则 ( 属性) ，该文件在 MSBuild 中使用并在生成过程中进行检测。 在 MSBuild 环境中，这些项的属性、项和元数据由生成系统使用。 *源文件* 中的每个宏都映射到由规则指定的 MSBuild 属性、项或项元数据。 默认情况下，如果不存在规则，则使用值 b 的名为的宏将转换为属性 A，其值为 B。初始转换步骤涉及到属性) 的关联属性 ( 文件 *中的或源文件* 到 MSBuild 语法的 NMake 语法映射。 *sources* NMake 文件中的每个宏都转换为属性文件中的属性， ( 属性) 。 在生成期间，将计算这些属性，并将某些属性的计算值映射到转换规则指定的各种其他属性、项或元数据。

例如， \_ \_ *源* 文件中的用户 C 标志宏用于指定在生成过程中要传递给编译器 ( # A0) 的命令行参数。 在 MSBuild 环境中，ClCompile 项列表包含要编译的源代码文件。 ClCompile 项列表由编译器在 [CL 任务](/visualstudio/msbuild/cl-task)中使用。 列表中每一项的其他元数据确定传递到编译器 ( # A0) 的其他标志。 因此，用户 \_ C 标志宏的值 \_ 应映射到 ClCompile 类型的项目的其他项元数据。 在初始转换步骤中， \_ 源文件中的用户 C \_ 标志宏会转换为 MSBuild 属性（也 \_ \_ 称为 *属性* 的生成文件中的用户 c 标志）。 在生成时将用户 C FLAGS 属性的计算值映射 \_ \_ 到其他元数据，如以下示例中所示：

```
  <!-- Contains rules to map compiler and linker switches -->
  <ItemDefinitionGroup>
    <ClCompile>
      ...
      <AdditionalOptions>%(AdditionalOptions) $(User_C_Flags)</AdditionalOptions>
      ...
    </ClCompile>
  </ItemDefinitionGroup>
```

前面的示例中所示的映射来自 PostToolsetRules. 属性文件。 示例映射使用 MSBuild ItemDefinitionGroup 来指定 \_ \_ 应在其他元数据内将 $ (用户 C 标记) 追加到 ClCompile 类型的所有项。 可以在 C： \\ Program 文件 (x86) \\ Windows 工具包 \\ 8.0 \\ bin \\ 转换目录中查找转换过程中使用的属性文件。

所有转换规则均使用标准 MSBuild 语法来指定。

## <a name="span-iddefault_conversion_rules_filespanspan-iddefault_conversion_rules_filespanspan-iddefault_conversion_rules_filespandefault-conversion-rules-file"></a><span id="Default_conversion_rules_file"></span><span id="default_conversion_rules_file"></span><span id="DEFAULT_CONVERSION_RULES_FILE"></span>默认转换规则文件


用于转换的默认规则是在 PostToolsetRules. 属性文件中指定的。 可以在 C： \\ Program 文件 (x86) \\ Windows 工具包 \\ 8.0 \\ bin \\ 转换目录中找到属性文件和其他转换属性文件。 可以使用 PostToolsetRules. 属性文件作为参考，为项目转换创建新规则。

## <a name="span-idcreating_custom_conversion_rulesspanspan-idcreating_custom_conversion_rulesspanspan-idcreating_custom_conversion_rulesspancreating-custom-conversion-rules"></a><span id="Creating_custom_conversion_rules"></span><span id="creating_custom_conversion_rules"></span><span id="CREATING_CUSTOM_CONVERSION_RULES"></span>创建自定义转换规则


默认规则文件 PostToolsetRules （属性）始终在转换过程中使用，但你也可以创建自己的自定义规则文件。 自定义规则文件为任何生成宏提供其他转换规则，该宏可能特定于以前生成该项目的生成环境。

Microsoft 提供的规则仅支持使用 Windows 7 WDK 中定义的宏和目标的项目的转换。 例如，这些规则仅支持出现在 *生成文件* 中的宏和目标。 不保证使用在前一生成环境中添加或修改的功能的任何项目的转换都是自动的。 作为一般规则，如果现有项目不会修改与项目相关联的源或 inc. 文件或由 WDK 安装的任何其他文件，则需要转换规则文件，这是不会修改 Windows 7 WDK 的全新安装。

自定义规则文件应遵循标准 MSBuild 语法，以及默认规则文件使用的设计模式。 默认规则应该提供充足的指导原则和示例，用于开发所有复杂的转换规则。

文件在中导入的顺序。.Vcxproj 文件和已检测的规则非常重要，应进行维护。 建议在 Microsoft 提供的 PostToolsetRules 后立即将用户开发的规则文件导入到项目中。属性：

```
  <Import Project="$(PostToolsetRules)" />
  <!-- Import PostToolsetRules to map nmake properties/macros to msbuild properties/items/metadata -->
```

## <a name="span-idconversion_tool_limitationsspanspan-idconversion_tool_limitationsspanspan-idconversion_tool_limitationsspanconversion-tool-limitations"></a><span id="Conversion_tool_limitations"></span><span id="conversion_tool_limitations"></span><span id="CONVERSION_TOOL_LIMITATIONS"></span>转换工具限制


NMake2MsBuild 实用工具不支持自定义目标的转换或某些非生成关键目标（如 BinPlace）的转换。 BinPlace 本身在 MSBuild.exe 环境中受支持，但不支持自动转换。 NMake2MsBuild 实用工具不提供在 Visual Studio 属性页中查看已转换项目的所有设置的功能。

## <a name="span-idnmake_syntax_and_behavior_not_supported_by_nmake2msbuildspanspan-idnmake_syntax_and_behavior_not_supported_by_nmake2msbuildspanspan-idnmake_syntax_and_behavior_not_supported_by_nmake2msbuildspannmake-syntax-and-behavior-not-supported-by-nmake2msbuild"></a><span id="NMake_syntax_and_behavior_not_supported_by_Nmake2Msbuild"></span><span id="nmake_syntax_and_behavior_not_supported_by_nmake2msbuild"></span><span id="NMAKE_SYNTAX_AND_BEHAVIOR_NOT_SUPPORTED_BY_NMAKE2MSBUILD"></span>Nmake2Msbuild 不支持 NMake 语法和行为


-   定义可选目录的推理规则中的宏引用扩展：

    ```
    INPUT_DIR= c:\MyDirectory
    .FromExt{$(INPUT_DIR)}.ToExt:
         cmd.exe /c echo  something 
    ```

    D 必须将上述更改为：

    ```
    .FromExt{ c:\MyDirectory}.ToExt:
         cmd.exe /c echo  something 
    ```

-   不支持 NMAKE 内联文件和宏替换。

    NMAKE 内联文件：请参阅 **创建内联文件文本**

    宏替换：请参阅 **宏替换**

    由于不支持内联文件和宏替换，因此以下目标将会正确转换：

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

-   **!** 不会转换错误语句。 MSBuild 中没有等效的等效项。
-   目标定义必须与调用目标的 NTTARGETFILE 宏匹配 1:1 \* ：不支持以下操作：

    ```
    Sources File:
    OBJ_NAME=Something
    NTTARGETFILES=$(_OBJ_DIR)\$(TARGET_DIRECTORY)\$(OBJ_NAME).obj
    Makefile.inc:
    obj\$(TARGET_DIRECTORY)\Something.obj : $(_OBJ_DIR)\$(TARGET_DIRECTORY)\$(Foo).obj
      
    ```

-   目标定义和 NTTARGETFILES 必须匹配;它们都应使用 $ (OBJ \_ NAME) .obj 或 *Somename*？ &lt;目标中的 $ 标记始终针对所有依赖项展开。

    有关详细信息，请参阅 **文件名宏** 。

-   $? 扩展到其时间戳晚于当前目标的所有依赖项。  对于转换后的项目，将忽略时间戳，并计算出所有依赖项。 这同样适用于 $&lt;

## <a name="span-idlimitations_of_converted_projectsspanspan-idlimitations_of_converted_projectsspanspan-idlimitations_of_converted_projectsspanlimitations-of-converted-projects"></a><span id="Limitations_of_Converted_Projects"></span><span id="limitations_of_converted_projects"></span><span id="LIMITATIONS_OF_CONVERTED_PROJECTS"></span>转换后的项目的限制


如果原始源文件文件有条件地编译了不同的一组文件，并且您通过在 IDE 中重命名/删除/添加文件来修改转换后的项目，则该项目将仅对更新的文件列表执行。 它将不再有条件地编译不同的文件。

转换的项目不支持与筛选文件。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Nmake2MsBuild](nmake2msbuild.md)

[从现有源文件创建驱动程序](/windows-hardware/drivers)

 

