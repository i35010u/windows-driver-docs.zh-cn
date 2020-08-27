---
title: 使用 AXE 创作测试
description: 使用 AXE 创作测试
ms.assetid: B042FE1B-98E4-48ae-BE2C-15C71EC6640A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff87e70579a89403434cd91aaa8ff1d6e6d3b52a
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902394"
---
# <a name="authoring-tests-in-axe"></a>使用 AXE 创作测试

TAEF 支持创作测试，这些测试在评估执行引擎 (AXE) 上执行。

TAEF 中的 AXE 支持使 TAEF 可以执行 AXE 评估清单。 它主要设计用于将传统测试（编写为命令行 Exe）包装到基于 XML 的 AXE 评估清单中。 这样，这些旧测试就可以通过 TAEF 执行，而无需重写测试来 TAEF 本机、托管或脚本测试。

## <a name="axe-tests-layout"></a>AXE 测试布局

尽管常规 TAEF 测试文件可以包含多个测试类和测试，但 TAEF AXE 测试 (由 AXE 评估清单定义的测试) 只能包含单个测试，因为清单会包装单个可执行文件。 因此，在 TAEF AXE 测试文件中查看测试时，您将始终看到测试文件 (这是您正在查看的 AXE 评估清单) 、包含单个测试类和单个测试：

``` syntax
te Examples\AXE.Basic.Examples.manifest /list
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
            Basic
                Basic::Basic

```

AXE 测试还不支持任何安装或清理方法。

## <a name="authoring-axe-tests"></a>创作 AXE 测试

对于 AXE 测试，TAEF 使用 AXE 评估清单文件格式。

## <a name="minimal-axe-test-file"></a>最小 AXE 测试文件

AXE 评估清单架构旨在支持非常丰富的复杂方案的复杂评估说明。 不过，这些清单也可能非常简单，因为有很少的必需节点。 下面的示例演示包含所有必需标记的最小清单。

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

AXE 测试评估文件是一个 XML 文件。 因此，它从普通 XML 标头开始 (**第1行**) 。

**第2行将** XML 文件标识为 AXE 清单。

**3-10 行** 为测试指定可用于唯一标识测试的标识和版本。

**第 12-19 行** 指定解释此清单和运行测试所需的 AXE 的最低版本。

**20-24 行** 为测试指定一个可读的名称和一个简短的工具提示说明。 请注意，查看测试属性时，测试类名称和测试名称将对应于 **ProgrammaticName** 元素值：

``` syntax
D:\enddev2.binaries.amd64chk\WexTest\CuE\TestExecution>te Examples\AXE.Basic.Examples.manifest /list
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
            Basic
                Basic::Basic

```

用户可读名称将分配给 **DisplayName** 属性。 这是由内部 TAEF 体系结构和设计引起的。

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

此评估会将名为 **AssessmentSample.exe**的简单的现有测试 EXE 打包。 **AssessmentSample.exe** 使用常见约定返回一个成功的进程退出代码，并返回一个非零值以指示失败。

**25-27 行** 告诉 AXE 和 TAEF，exit 值为零表示测试成功，任何其他值表示失败。

最后， **28-32 行** 指示 AXE 使用 Win32 API CreateProcess ( # A1 来执行 **AssessmentSample.exe**。

## <a name="using-metadata-in-axe-test-file"></a>在 AXE 测试文件中使用元数据

对于任何其他 TAEF 测试，还可以将元数据应用于 TAEF AXE 测试。 请看下面所示的示例。

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

第**25-29 行**演示了如何将 TAEF 标准和自定义元数据应用于 AXE 测试。 " **AxeAssessmentManifest** XML" 节点下的 " **属性** " 节点。 " **属性** " 节点下的单个级别 XML 标记被识别为元数据 (属性) 。 " **属性** " 下的所有单级 XML 标记均被解释为属性名称，其文本值被解释为属性值。 在上面的示例中，" **所有者** " 解释为属性名称，而 " **用户** " 作为属性值。 这些元素中没有文本的 XML 标记被解释为其值等于空字符串的元素 (例如** &lt; SimpleTagWithNoText/ &gt; **) 。 忽略 **属性** 下的多级 XML 标记 (例如，多级标记，如

```cpp
<VerifyOSVersion>
    <Major>6</Major>
    <Minor>0</Minor>
    <Build>0</Build>
</VerifyOSVersion>
```

将忽略) 。 类似于任何其他 TAEF 测试，可使用 **/listProperties** 选项显示 TAEF 元数据：

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

## <a name="axe-tests-metadata-support-limitations"></a>AXE 测试元数据支持限制

>[!NOTE]
>并非所有 TAEF 标准测试元数据都可与 TAEF AXE 测试一起使用。

- 旨在修改执行进程的环境（例如 **ActivationContext** 和 **ThreadingModel**）的所有元数据不能用于 AXE 测试。 AXE 不使用 TAEF 的进程来执行测试，而是创建一个新的进程，在该进程中，它会运行 AXE 测试文件指定的可执行程序， (AXE 评估清单) 。 由于同样的原因，数据驱动的 TAEF 测试 (数据 **源** 属性) 无法与 AXE TAEF 测试一起使用。
- 同样，由于 TAEF AXE 测试文件只能封装一个测试，因此，修改与其他测试（如 **ExecutionGroup**）相关的测试行为的 TAEF 元数据也将不起作用。
- 由于 AXE 的体系结构，AXE 只能运行提升的进程。 因此，正如你在上面的 TAEF AXE test "属性中看到的那样，每个 TAEF AXE 测试都具有已应用的 **属性 \[ RunAs \] =** 。

## <a name="axe-test-file-with-runtime-parameters"></a>包含运行时参数的 AXE 测试文件

TAEF AXE 测试还支持运行时参数。 若要将 TAEF 的运行时参数用于 AXE 测试，需要在 AXE 测试文件中定义要传递到可执行程序的参数名称。

它超出了本文档的范围，描述所有详细信息中所有可能的 AXE 清单参数功能。 有关此信息，请参阅 AXE 评估文档。 本文档将仅涵盖最常见和有用的参数应用程序。

下面的示例演示一个更复杂的 AXE 评估清单。

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

**行 25-62** 是一些参数定义，用于描述 TAEF 和 AXE 用于将数据传递到评估可执行文件的参数。

最简单的参数定义位于 **26-36 行**。 它包含与清单的 "**描述**" 部分完全相同的必需**说明**部分，如上所述。 然后，会看到定义参数数据类型的 **类型** 标记。  (请参阅 AXE 评估文档以了解所有支持的数据类型。 ) 

可选的 **CommandLineFormat** 部分介绍了如何为评估命令行设置评估参数的格式。 此 XML 节点必须包含一个为有效 .NET 格式字符串的非空字符串。 评估参数值将是传递到格式化程序的唯一对象。 这意味着，格式字符串必须包含一个且只能包含一个索引为零的复合格式项。 一些示例包括：-input {0} 、/affinity： 0x {0，X} 或-InputFile = " {0} "。

下一个参数在 **行 37-48** 上定义，并且是必需的参数。 它在上一个参数中的定义的唯一区别是可选的 **必需** 标记。 此标记指示 AXE 要求用户在 AXE 测试执行期间传递此参数。 如果省略此参数，则将使用该参数的数据类型的默认值 (例如，INT 表示 INT，空字符串表示字符串，等等) 。

最后，该示例中的最后一个参数指定一个可选的 **DefaultValue** 标记，该标记描述参数的默认值。 如果此节点为空，则将参数的数据类型的默认值用作默认值。 上面的示例使用 "% AssessmentResultsPath%"，这是一个在评估开始执行时由 AXE 设置的环境变量。 同样，请参阅 AXE 评估文档以了解所有支持的 AXE 环境变量。

参数按定义的反向顺序传递到可执行文件-在文件中定义的参数将首先传递到可执行文件。

通过使用 **/p**命令行选项) ，你可以将 TAEF AXE[运行时参数](runtime-parameters.md)测试作为任何其他使用运行时 (参数的 TAEF 测试执行：

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

## <a name="axe-test-cross-machine-execution"></a>AXE 测试跨计算机执行

[对于跨计算机执行方案](cross-machine-execution.md)，TAEF 将尝试确定需要部署的测试依赖项，以及测试是否成功执行。 对于 AXE 测试文件，TAEF 会将位于同一文件夹中的所有文件都与 TAEF AXE 测试一起复制到远程计算机上执行。

当前不支持跨计算机执行 AXE 测试到 ARM 平台。

## <a name="taef-axe-support-dependencies"></a>TAEF AXE 支持依赖项

AXE 不随 Windows 提供。 若要执行 AXE 测试，需要将 **axecore.dll** 和 **Microsoft.Assessment.dll** 复制到 TAEF 或 TAEF AXE 测试目录。
