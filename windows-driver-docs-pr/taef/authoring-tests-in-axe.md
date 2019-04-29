---
title: 使用 AXE 创作测试
description: 使用 AXE 创作测试
ms.assetid: B042FE1B-98E4-48ae-BE2C-15C71EC6640A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 336bf4b0eff08ceda7b978660bcd2bf5dab9141b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372742"
---
# <a name="authoring-tests-in-axe"></a>使用 AXE 创作测试


TAEF 支持创作测试执行与将评估执行引擎 （斧头磨快）。

斧头磨快中 TAEF 支持 TAEF 执行斧头磨快评估清单。 它主要用于包装旧测试，作为命令行的 Exe，写入到基于 XML 的斧头磨快评估清单。 在这种方式，这些旧测试会成为 TAEF 与可执行文件而无需重写到 TAEF 本机，测试管理，或编写脚本的测试。

## <a name="span-idaxetestslayoutspanspan-idaxetestslayoutspanspan-idaxetestslayoutspanaxe-tests-layout"></a><span id="AXE_Tests_Layout"></span><span id="axe_tests_layout"></span><span id="AXE_TESTS_LAYOUT"></span>斧头磨快测试布局


尽管常规 TAEF 测试文件可以包含多个测试类和测试，但 TAEF 斧头磨快测试 （由斧头磨快评估清单定义的测试） 可以包含一个测试，因为将该清单将对单个可执行文件。 因此，当 TAEF 斧头磨快测试文件中查看测试，将始终看到测试文件 （这是你正在查看的斧头磨快评估清单），包含单个测试类和一个测试：

``` syntax
te Examples\AXE.Basic.Examples.manifest /list
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
            Basic
                Basic::Basic

```

斧头磨快测试也不支持安装或清理的任何方法。

## <a name="span-idauthoringaxetestsspanspan-idauthoringaxetestsspanspan-idauthoringaxetestsspanauthoring-axe-tests"></a><span id="Authoring_AXE_Tests"></span><span id="authoring_axe_tests"></span><span id="AUTHORING_AXE_TESTS"></span>创作斧头磨快测试


对于斧头磨快测试，TAEF 使用斧头磨快评估清单文件格式。

## <a name="span-idminimalaxetestfilespanspan-idminimalaxetestfilespanspan-idminimalaxetestfilespanminimal-axe-test-file"></a><span id="Minimal_AXE_Test_File"></span><span id="minimal_axe_test_file"></span><span id="MINIMAL_AXE_TEST_FILE"></span>最小斧头磨快测试文件


斧头磨快评估清单架构旨在支持非常丰富的复杂评估说明复杂的方案。 但是，清单还可以非常简单因为有很少的必需节点。 下面的示例显示了包含所有必需的标记的最小清单。

```cpp
1<?xml version="1.0" encoding="utf-8"?>
2<AxeAssessmentManifest xmlns="http://www.microsoft.com/axe/assessment/manifest">
3  <VersionedId>
4    <Guid>{ABCBFDE6-D731-4030-9049-E7CAAB6A6EEE}</Guid>
5    <Version>
6      <Major>1</Major>
7      <Minor>0</Minor>
8      <Build>0</Build>
9      <Revision>0</Revision>
10    </Version>
11  </VersionedId>
12  <MinimumAxeVersionRequired>
13    <Version>
14      <Major>1</Major>
15      <Minor>0</Minor>
16      <Build>1</Build>
17      <Revision>0</Revision>
18    </Version>
19  </MinimumAxeVersionRequired>
20  <Description>
21    <ProgrammaticName>Basic</ProgrammaticName>
22    <DisplayName>Basic Examples</DisplayName>
23    <ToolTip>Sample Basic Examples Assessment Tooltip</ToolTip>
24  </Description>
25  <Meta>
26    <ExitValueMeaning> <ZeroIsSuccess/> </ExitValueMeaning>
27  </Meta>
28  <Execution>
29    <CreateProcess>
30      <ApplicationName>AssessmentSample.exe</ApplicationName>
31    </CreateProcess>
32  </Execution>
33</AxeAssessmentManifest>
```

将斧头磨快测试评估文件是一个 XML 文件。 因此，它将开始使用普通的 XML 标头 (**行 1**)。

**第 2 行**标识斧头磨快清单的 XML 文件。

**行 3 10**标识和可用于唯一标识该测试的版本都进行测试。

**行 12-19**指定斧头磨快将解释此清单并运行测试所需的最低版本。

**行 20 到 24 个**人工可读名称和简短的工具提示说明都进行测试。 请注意，当您查看测试属性，你的测试类名称和你的测试名称将对应于**ProgrammaticName**元素的值：

``` syntax
D:\enddev2.binaries.amd64chk\WexTest\CuE\TestExecution>te Examples\AXE.Basic.Examples.manifest /list
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
            Basic
                Basic::Basic

```

用户可读名称分配给**DisplayName**属性。 此分配是由于内部 TAEF 体系结构和设计。

``` syntax
Te Examples\AXE.Basic.Examples.manifest /listproperties
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
                Property[TaefTestType] =  AxeAssessment

            Basic
                Basic::Basic
                        Property[DisplayName] =  Basic Examples
                        Property[ProgrammaticName] =  Basic
                        Property[RunAs] =  Elevated
                        Property[ToolTip] =  Sample Basic Examples Assessment Tooltip

```

此评估包装一个简单的和现有测试名为 EXE **AssessmentSample.exe**。 **AssessmentSample.exe**使用通用约定返回零表示成功和失败的一个非零值的进程退出代码。

**行 25 27**告诉斧头磨快和 TAEF 为退出值时为零表示测试成功，任何其他值表示失败。

最后，**行 28-32**指示斧头磨快使用 Win32 API createprocess （） 来执行**AssessmentSample.exe**。

## <a name="span-idusingmetadatainaxetestfilespanspan-idusingmetadatainaxetestfilespanspan-idusingmetadatainaxetestfilespanusing-metadata-in-axe-test-file"></a><span id="Using_Metadata_in_AXE_Test_File"></span><span id="using_metadata_in_axe_test_file"></span><span id="USING_METADATA_IN_AXE_TEST_FILE"></span>使用斧头磨快测试文件中的元数据


与任何其他 TAEF 测试一样，向 TAEF 斧头磨快测试，还可以应用元数据。 请考虑如下所示的示例。

```cpp
1<?xml version="1.0" encoding="utf-8"?>
2<AxeAssessmentManifest xmlns="http://www.microsoft.com/axe/assessment/manifest">
3  <VersionedId>
4    <Guid>{F310F3F6-F786-4118-8A18-BC020C7D2521}</Guid>
5    <Version>
6      <Major>1</Major>
7      <Minor>0</Minor>
8      <Build>0</Build>
9      <Revision>0</Revision>
10    </Version>
11  </VersionedId>
12  <MinimumAxeVersionRequired>
13    <Version>
14      <Major>1</Major>
15      <Minor>0</Minor>
16      <Build>1</Build>
17      <Revision>0</Revision>
18    </Version>
19  </MinimumAxeVersionRequired>
20  <Description>
21    <ProgrammaticName>CustomMetadataExamples</ProgrammaticName>
22    <DisplayName>Custom Metadata Examples</DisplayName>
23    <ToolTip>Sample Custom Metadata Examples Assessment Tooltip</ToolTip>
24  </Description>
25  <Properties>
26    <Owner>Someone</Owner>
27    <Priority>1</Priority>
28    <Parallel>false</Parallel>
29  </Properties>
30  <Meta>
31    <ExitValueMeaning> <ZeroIsSuccess/> </ExitValueMeaning>
32  </Meta>
33  <Execution>
34    <CreateProcess>
35      <ApplicationName>AssessmentSample.exe</ApplicationName>
36    </CreateProcess>
37  </Execution>
38</AxeAssessmentManifest>
```

**行 25 日-29**演示可以如何应用 TAEF 标准和自定义元数据到斧头磨快的测试。 下**AxeAssessmentManifest** XML 节点是**属性**节点。 单个级别 XML 标记下**属性**节点识别为元数据 （属性）。 所有单个级别 XML 标记下**属性**解释为属性名称和其值被解释为属性值的文本。 在上述示例中，**所有者**被解释为属性名称和**有人**作为属性值。 在这些元素中没有文本的 XML 标记将被解释为它的值等于空字符串的元素 (例如，  **&lt;SimpleTagWithNoText /&gt;**)。 多级 XML 标记下**属性**忽略 （例如，多层的标签，如

```cpp
<VerifyOSVersion>
    <Major>6</Major>
    <Minor>0</Minor>
    <Build>0</Build>
</VerifyOSVersion>
```

将被忽略）。 使用与任何其他 TAEF 测试类似， **/listProperties**选项以显示 TAEF 元数据：

``` syntax
te Examples\AXE.CustomMetadata.Examples.manifest /listProperties
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64

        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.CustomMetadata.Examples.manifest
                Property[TaefTestType] =  AxeAssessment

            CustomMetadataExamples
                CustomMetadataExamples::CustomMetadataExamples
                        Property[DisplayName] =  Custom Metadata Examples
                        Property[Owner] =  Someone
                        Property[Parallel] =  false
                        Property[Priority] =  1
                        Property[ProgrammaticName] =  CustomMetadataExamples
                        Property[RunAs] =  Elevated
                        Property[ToolTip] =  Sample Custom Metadata Examples Assessment Tooltip


```

## <a name="span-idaxetestsmetadatasupportlimitationsspanspan-idaxetestsmetadatasupportlimitationsspanspan-idaxetestsmetadatasupportlimitationsspanaxe-tests-metadata-support-limitations"></a><span id="AXE_Tests_Metadata_Support_Limitations"></span><span id="axe_tests_metadata_support_limitations"></span><span id="AXE_TESTS_METADATA_SUPPORT_LIMITATIONS"></span>斧头磨快测试元数据支持限制


注意：使用 TAEF 斧头磨快测试，可以使用不是所有 TAEF 标准测试元数据。

-   修改执行的环境中的过程，如旨在所有元数据**ActivationContext**并**ThreadingModel**，不会使用斧头磨快测试。 斧头磨快不使用 TAEF 的过程来执行测试，但创建一个新的进程在其中运行指定的可执行程序斧头磨快测试文件 （斧头磨快评估清单）。 出于相同原因，数据驱动 TAEF 测试 (**数据源**属性) 并不适用于斧头磨快 TAEF 测试或者。
-   类似地，因为 TAEF 斧头磨快测试文件可以封装仅一个测试，TAEF 元数据的修改与其他测试，测试的行为如**ExecutionGroup**，也不会工作。
-   由于斧头磨快体系结构，斧头磨快只能运行提升的进程。 因此，正如您看到从上述 TAEF 斧头磨快测试属性，每个 TAEF 斧头磨快测试都有**属性\[RunAs\] = 提升**应用。

## <a name="span-idaxetestfilewithruntimeparametersspanspan-idaxetestfilewithruntimeparametersspanspan-idaxetestfilewithruntimeparametersspanaxe-test-file-with-runtime-parameters"></a><span id="AXE_Test_File_with_Runtime_Parameters"></span><span id="axe_test_file_with_runtime_parameters"></span><span id="AXE_TEST_FILE_WITH_RUNTIME_PARAMETERS"></span>使用运行时参数斧头磨快测试文件


TAEF 斧头磨快测试还支持运行时参数。 若要使用斧头磨快测试 TAEF 的运行时参数，需要斧头磨快测试文件中定义要传递给可执行程序的参数名称。

它不在本文档描述的所有可能的斧头磨快清单参数功能中的所有详细信息的范围。 有关该信息，请参阅斧头磨快评估文档。 本文档仅涵盖最常见和有用参数应用程序。

下面的示例演示一个更复杂的斧头磨快评估清单。

```cpp
1<?xml version="1.0" encoding="utf-8"?>
2<AxeAssessmentManifest xmlns="http://www.microsoft.com/axe/assessment/manifest">
3  <VersionedId>
4    <Guid>{B63B2FFF-EDEB-41FB-92EA-529CE4A46D20}</Guid>
5    <Version>
6      <Major>1</Major>
7      <Minor>0</Minor>
8      <Build>0</Build>
9      <Revision>0</Revision>
10    </Version>
11  </VersionedId>
12  <MinimumAxeVersionRequired>
13    <Version>
14      <Major>1</Major>
15      <Minor>0</Minor>
16      <Build>1</Build>
17      <Revision>0</Revision>
18    </Version>
19  </MinimumAxeVersionRequired>
20  <Description>
21    <ProgrammaticName>ExplicitRuntimeParameters</ProgrammaticName>
22    <DisplayName>Explicit Runtime Parameters</DisplayName>
23    <ToolTip>Sample Explicit Runtime Parameters Assessment Tooltip</ToolTip>
24  </Description>
25  <ParameterDefinitions>
26    <ParameterDefinition>
27      <Description>
28        <ProgrammaticName>SimpleParameter</ProgrammaticName>
29        <DisplayName>Simple parameter</DisplayName>
30        <ToolTip>The is an example of a simple parameter.</ToolTip>
31      </Description>
32      <Type>
33        <String></String>
34      </Type>
35      <CommandLineFormat>{0}</CommandLineFormat>
36    </ParameterDefinition>
37    <ParameterDefinition>
38      <Description>
39        <ProgrammaticName>RequiredParameterWithoutDefaultValue</ProgrammaticName>
40        <DisplayName>Required parameter without a default value.</DisplayName>
41        <ToolTip>The is an example of a required parameter Without a default value.</ToolTip>
42      </Description>
43      <Required>True</Required>
44      <Type>
45        <Int></Int>
46      </Type>
47      <CommandLineFormat>{0}</CommandLineFormat>
48    </ParameterDefinition>
49    <ParameterDefinition>
50      <Description>
51        <ProgrammaticName>RequiredParameterWithDefaultValue</ProgrammaticName>
52        <DisplayName>Required parameter with a default value</DisplayName>
53        <ToolTip>The is an example of a required parameter With a default value.</ToolTip>
54      </Description>
55      <Required></Required>
56      <DefaultValue>"%AssessmentResultsPath%"</DefaultValue>
57      <Type>
58        <String></String>
59      </Type>
60      <CommandLineFormat>/RequiredParameterWithDefaultValue={0}</CommandLineFormat>
61    </ParameterDefinition>
62  </ParameterDefinitions>
63  <Meta>
64    <ExitValueMeaning> <ZeroIsSuccess/> </ExitValueMeaning>
65  </Meta>
66  <Execution>
67    <CreateProcess>
68      <ApplicationName>AssessmentSample.exe</ApplicationName>
69    </CreateProcess>
70  </Execution>
71</AxeAssessmentManifest>
```

**行 25 62**是描述由 TAEF 和斧头磨快用于将数据传递到评估可执行文件的参数的参数定义。

最简单的参数定义是在**行 26 36**。 它包含一种必要**说明**正是与相同的部分**说明**上文所述的清单的部分。 然后，请参阅**类型**定义的参数数据类型的标记。 （请参阅所有受支持的数据类型斧头磨快评估文档）。

可选**CommandLineFormat**部分介绍如何评估命令行设置评估参数的格式。 此 XML 节点必须包含有效的.NET 格式设置字符串的非空字符串。 评估参数值将传递给格式化程序的唯一对象。 这意味着在格式设置字符串必须包含一个且只有一个复合格式设置与索引零开始的项。 下面是一些示例:-输入{0}，/affinity:0 x {0，X}，或-输入文件 ="{0}"。

下一个参数定义上**行 37 48**和参数是必需的。 在上一个参数从其定义中的唯一区别是一个可选**所需**标记。 此标记指示斧头磨快需要让用户在斧头磨快测试执行过程中传递此参数。 如果省略此参数，然后参数的数据类型的默认值将用作 （例如，int 类型的零、 空字符串的字符串，等等）。

最后，在示例中的最后一个参数指定一个可选**DefaultValue**标记，它描述参数的默认值。 如果此节点为空，参数的数据类型的默认值将用作默认值。 上面的示例使用"%assessmentresultspath%"，这是由斧头磨快评估开始执行时设置的环境变量。 适用于所有受支持斧头磨快环境变量，请参阅斧头磨快评估文档。

传递到其定义的相反顺序的可执行文件的参数-在文件中定义的参数上一次传递可执行文件的第一次。

执行 TAEF 斧头磨快[运行时参数](runtime-parameters.md)为使用运行时参数的任何其他 TAEF 测试的测试 (通过使用 **/p**命令行选项):

``` syntax
te AXE.ExplicitRuntimeParameters.Examples.manifest /p:SimpleParameter=Test1 /p:RequiredParameterWithoutDefaultValue=10
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64

ExplicitRuntimeParameters::ExplicitRuntimeParameters
AssessmentSample.exe is simple application for AXE assessment demo.
It just echoes the arguments passed to it to the console.

Parameters passed from the command line:
Argument[0]=AssessmentSample.exe
Argument[1]=10
Argument[2]=/RequiredParameterWithDefaultValue=C:\Results\JobResults_DEVRH_2011-0129_0250-12.394\0
Argument[3]=Test1

FileName: C:\Results\JobResults_DEVRH_2011-0129_0250-12.394\JobResults_DEVRH_2011-0129_0250-12.394.xml
Saved output file to: D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\WexLogFileOutput\
000001_~ExplicitRuntimeParameters_JobResults_DEVRH_2011-0129_0250-12.394.xml
EndGroup: ExplicitRuntimeParameters::ExplicitRuntimeParameters [Passed]

```

## <a name="span-idaxetestcrossmachineexecutionspanspan-idaxetestcrossmachineexecutionspanspan-idaxetestcrossmachineexecutionspanaxe-test-cross-machine-execution"></a><span id="AXE_Test_Cross_Machine_Execution"></span><span id="axe_test_cross_machine_execution"></span><span id="AXE_TEST_CROSS_MACHINE_EXECUTION"></span>跨计算机执行斧头磨快测试


[对于跨计算机执行方案](cross-machine-execution.md)，TAEF 尝试确定需要与成功的测试执行的测试一起部署的测试依赖项。 斧头磨快测试文件中，对于 TAEF 将复制与 TAEF 斧头磨快测试到远程计算机上执行的相同文件夹中的所有文件。

跨计算机执行到 ARM 斧头磨快测试平台是当前不支持。

## <a name="span-idtaefaxesupportdependenciesspanspan-idtaefaxesupportdependenciesspanspan-idtaefaxesupportdependenciesspantaef-axe-support-dependencies"></a><span id="TAEF_AXE_Support_Dependencies"></span><span id="taef_axe_support_dependencies"></span><span id="TAEF_AXE_SUPPORT_DEPENDENCIES"></span>TAEF 斧头磨快支持依赖项


斧头磨快未随 Windows。 若要能够执行斧头磨快测试，需要复制**axecore.dll**并**Microsoft.Assessment.dll** TAEF 或 TAEF 斧头磨快测试目录。









