---
title: 标准测试元数据
description: 标准测试元数据
ms.assetid: A95FC176-B3A1-4bbf-833E-411CDE73C571
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e951d50c37e5dbe21fc741bc5ca7937cea40d15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372991"
---
# <a name="standard-test-metadata"></a>标准测试元数据


以下测试标记 up 元数据是可应用于 TAEF 测试的标准元数据。

## <a name="span-idimplicitmetadataspanspan-idimplicitmetadataspanspan-idimplicitmetadataspanimplicit-metadata"></a><span id="Implicit_Metadata"></span><span id="implicit_metadata"></span><span id="IMPLICIT_METADATA"></span>隐式元数据


某些信息的元数据自动进行推断的标记测试：

-   "Name"的测试的完全限定的名称。
-   "体系结构"-DLL 的处理器体系结构。 此值将为 x86、 x64 或 arm 之一。
-   "TestFile"的测试中所述的 DLL 文件。

## <a name="span-idselectionmetadataspanspan-idselectionmetadataspanspan-idselectionmetadataspanselection-metadata"></a><span id="Selection_Metadata"></span><span id="selection_metadata"></span><span id="SELECTION_METADATA"></span>所选内容元数据


所选内容元数据是只需首选部分的元数据以允许团队具有标准，以允许他们以更好地使用他人的测试。 没有任何所需的元数据-首要位置元数据会增加添加自动化的成本和所有元数据应为可选的或应启用选择加入的行为。

有些情况下针对元数据值可以指定多个值，这种情况下应使用分号分隔的列表，并使用包含样式选择查询，若要为其测试。 例如，如果"所有者"元数据需要两个值，则它应被设置为"Someone;SomeoneElse"。 将查询来选择仅由人员拥有的测试：

``` syntax
te Wex.Common.Tests.dll /select:@Owner='Someone'
```

而下面的查询将选择拥有或由人共同拥有的测试：

``` syntax
te Wex.Common.Tests.dll /select:@Owner='*Someone*'
```

您可以定义自己的元数据以在你自己的公司内使用。 以下建议是一些建议。 .

## <a name="span-idyoushouldmetadataspanspan-idyoushouldmetadataspanspan-idyoushouldmetadataspanyou-should-metadata"></a><span id="_You_should...__Metadata"></span><span id="_you_should...__metadata"></span><span id="_YOU_SHOULD...__METADATA"></span>"您应该..."元数据


这些元数据属性是一些建议，并具有明确的含义。 根据你的需要请使用这些元数据属性：

<span id="_ActivationContext_"></span><span id="_activationcontext_"></span><span id="_ACTIVATIONCONTEXT_"></span>"ActivationContext"  
指定系统中的二进制文件从各种通过并行程序集的特定版本。 请参阅[激活上下文](activation-context.md)有关详细信息。

<span id="_BinaryUnderTest_"></span><span id="_binaryundertest_"></span><span id="_BINARYUNDERTEST_"></span>"BinaryUnderTest"  
一个给定测试的二进制\[单元\]测试。 这允许开发人员能够快速运行验证给定的 DLL 的所有单元测试。

<span id="_DefaultTestResult_"></span><span id="_defaulttestresult_"></span><span id="_DEFAULTTESTRESULT_"></span>"DefaultTestResult"  
为给定的测试覆盖"通过"的默认测试的结果。 如果测试通过，记录的结果将是默认测试结果。 可能的值为"通过"、"失败"、"未运行"、"已阻止"和"跳过"。

<span id="_DeploymentItem_"></span><span id="_deploymentitem_"></span><span id="_DEPLOYMENTITEM_"></span>["DeploymentItem"](deploymentitem-metadata.md)  
标识为测试依赖项的文件和文件夹。

<span id="_Description_"></span><span id="_description_"></span><span id="_DESCRIPTION_"></span>"Description"  
对测试任务的简短描述。

<span id="_DpiAware_"></span><span id="_dpiaware_"></span><span id="_DPIAWARE_"></span>"DpiAware"  
当设置为"true"，TAEF 将标记为 DPI 感知的进程中运行测试时，请参阅[高 DPI](https://docs.microsoft.com/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)。

<span id="_ExecutionGroup_"></span><span id="_executiongroup_"></span><span id="_EXECUTIONGROUP_"></span>"ExecutionGroup"  
一组连续测试的类中需要按顺序运行，如果在执行组中以前的测试则将阻止未运行，否则将失败。 请参阅[执行组](execution-groups.md)有关详细信息。

<span id="_Ignore_"></span><span id="_ignore_"></span><span id="_IGNORE_"></span>"Ignore"  
测试类或"忽略"元数据设置为"true"时将跳过执行测试方法或按 TAEF 列出。 若要重写此行为并运行或列出包括使用"忽略"元数据的所有测试，请指定 **/runIgnoredTests**作为命令行参数。

<span id="_IsolationLevel_"></span><span id="_isolationlevel_"></span><span id="_ISOLATIONLEVEL_"></span>"IsolationLevel"  
指定的最小执行 TAEF 测试时要使用的隔离级别。 请参阅[测试隔离](test-isolation.md)的更多详细信息。

<span id="_Parallel_"></span><span id="_parallel_"></span><span id="_PARALLEL_"></span>["Parallel"](parallel.md)  
在多个处理器上并行执行测试。 有关更多详细信息，请参阅[并行](parallel.md)。

<span id="_Priority_"></span><span id="_priority_"></span><span id="_PRIORITY_"></span>"Priority"  
较小的整数作为测试的优先级是高优先级。

<span id="_RebootPossible_"></span><span id="_rebootpossible_"></span><span id="_REBOOTPOSSIBLE_"></span>["RebootPossible"](reboot.md)  
重新启动 Api 来请求 TAEF 执行重启计算机，或通知即将发生的测试启动重启 TAEF 使用何时设置为 true，。

<span id="_RunAs_"></span><span id="_runas_"></span><span id="_RUNAS_"></span>"RunAs"  
指定应在其中运行的测试中关注的上下文。 请参阅[运行方式执行](runas.md)有关详细信息。

<span id="_RunFixtureAs_"></span><span id="_runfixtureas_"></span><span id="_RUNFIXTUREAS_"></span>["RunFixtureAs"](runfixtureas.md)  
指定应在其中运行测试装置中问题的上下文。 请参阅[RunFixtureAs](runfixtureas.md)有关详细信息。

<span id="_TestClassification_Scope_"></span><span id="_testclassification_scope_"></span><span id="_TESTCLASSIFICATION_SCOPE_"></span>"TestClassification:Scope"  
"作用域"的测试分类标识用于验证"工程处理事件"的测试附件在 Windows 中发生的。

<span id="_TestClassification_Type_"></span><span id="_testclassification_type_"></span><span id="_TESTCLASSIFICATION_TYPE_"></span>"TestClassification:Type"  
测试分类"类型"标识类型的需要是可分辨的测试。

<span id="_TestClassification_"></span><span id="_testclassification_"></span><span id="_TESTCLASSIFICATION_"></span>"TestClassification"  
使用属性值"单元： WUTG"来指示符合到 Windows 单元测试指导原则 (WUTG) 的单元测试。 使用属性值"单元： WUTG:ChexGate"来指示符合到 Windows 单元测试指导原则 (WUTG)，应在封闭 Chex 方案 （阻止提交失败） 的阶段运行的单元测试。

<span id="_TestTimeout_"></span><span id="_testtimeout_"></span><span id="_TESTTIMEOUT_"></span>"TestTimeout"  
指定的最大给定的测试或安装程序/清理方法可以采用的时间量。 请参阅[超时](taef-timeouts.md)有关详细信息。

<span id="_ThreadingModel_"></span><span id="_threadingmodel_"></span><span id="_THREADINGMODEL_"></span>"ThreadingModel"  
预配置 COM 线程模型的测试使用的。 请参阅[配置线程模型](threading-models.md)有关详细信息。

数据驱动的测试相关：

<span id="_DataSource_"></span><span id="_datasource_"></span><span id="_DATASOURCE_"></span>"DataSource"  
指定的数据的主要来源[数据驱动的测试](data-driven-testing.md)。

<span id="_TableId_"></span><span id="_tableid_"></span><span id="_TABLEID_"></span>"TableId"  
指定的名称或从"数据源"的情况下单独的表的 Id[表基于数据驱动测试](table-data-source.md)。

<span id="_Pict_Timeout___and_deprecated__PictTimeout__"></span><span id="_pict_timeout___and_deprecated__picttimeout__"></span><span id="_PICT_TIMEOUT___AND_DEPRECATED__PICTTIMEOUT__"></span>"Pict： 超时"（和已弃用"PictTimeout"）  
重写 PICT.exe 处理用户指定的模型文件的情况下允许的 5 分钟的默认超时值[PICT 基于数据驱动的测试](pict-data-source.md)。

<span id="_Pict_SeedingFile___and_deprecated__Seed__"></span><span id="_pict_seedingfile___and_deprecated__seed__"></span><span id="_PICT_SEEDINGFILE___AND_DEPRECATED__SEED__"></span>"Pict: SeedingFile"（和已弃用"种子"）  
指定的相对位置到种子文件中，从"数据源"的情况下单独[PICT 基于数据驱动的测试](pict-data-source.md)。

<span id="_Pict_Order_"></span><span id="_pict_order_"></span><span id="_PICT_ORDER_"></span>"Pict:Order"  
调用时指定 PICT.exe /o 参数的值[PICT 基于数据驱动的测试](pict-data-source.md)。

<span id="_Pict_ValueSeparator_"></span><span id="_pict_valueseparator_"></span><span id="_PICT_VALUESEPARATOR_"></span>"Pict:ValueSeparator"  
调用时指定 PICT.exe /d 参数的值[PICT 基于数据驱动的测试](pict-data-source.md)。

<span id="_Pict_AliasSeparator_"></span><span id="_pict_aliasseparator_"></span><span id="_PICT_ALIASSEPARATOR_"></span>"Pict:AliasSeparator"  
调用时为 PICT.exe 指定/a 参数的值[PICT 基于数据驱动的测试](pict-data-source.md)。

<span id="_Pict_NegativeValuePrefix_"></span><span id="_pict_negativevalueprefix_"></span><span id="_PICT_NEGATIVEVALUEPREFIX_"></span>"Pict:NegativeValuePrefix"  
调用时指定 PICT.exe /n 参数的值[PICT 基于数据驱动的测试](pict-data-source.md)。

<span id="_Pict_Random_"></span><span id="_pict_random_"></span><span id="_PICT_RANDOM_"></span>"Pict:Random"  
指定调用的 PICT.exe 时是否应使用随机性[PICT 基于数据驱动的测试](pict-data-source.md)。 在这种情况，是由 TAEF 记录使用的随机种子。

<span id="_Pict_RandomSeed_"></span><span id="_pict_randomseed_"></span><span id="_PICT_RANDOMSEED_"></span>"Pict:RandomSeed"  
调用时为 PICT.exe 指定 /r 参数的值[PICT 基于数据驱动的测试](pict-data-source.md)。 将此项设置更改的默认值为"Pict： 随机"从 false 到 true。

<span id="_Pict_CaseSensitive_"></span><span id="_pict_casesensitive_"></span><span id="_PICT_CASESENSITIVE_"></span>"Pict: CaseSensitive"  
指定调用时，是否应为 PICT.exe 使用 /c 参数[PICT 基于数据驱动的测试](pict-data-source.md)。

针对设备相关的支持：

<span id="_TestResourceDependent_"></span><span id="_testresourcedependent_"></span><span id="_TESTRESOURCEDEPENDENT_"></span>"TestResourceDependent"  
指定当前作用域中的测试依赖于 TestResource 和 BuildResourceList(...) 所收集的资源的函数。请参阅[对设备的支持](device-support.md)有关详细信息。

<span id="_ResourceSelection_"></span><span id="_resourceselection_"></span><span id="_RESOURCESELECTION_"></span>"ResourceSelection"  
指定要匹配 TestResources BuildResourceList(...) 所收集的测试有问题的相关的查询。 请参阅[对设备的支持](device-support.md)有关详细信息。

## <a name="span-idyoucanmetadataspanspan-idyoucanmetadataspanspan-idyoucanmetadataspanyou-can-metadata"></a><span id="_You_can...__Metadata"></span><span id="_you_can...__metadata"></span><span id="_YOU_CAN...__METADATA"></span>"您可以..."元数据


可以使用这些元数据属性，但不是保证其解释;如果他们想要团队可以使用它们。

<span id="_Owner_"></span><span id="_owner_"></span><span id="_OWNER_"></span>"所有者"  
测试的所有者的别名。

<span id="_ProcessUnderTest_"></span><span id="_processundertest_"></span><span id="_PROCESSUNDERTEST_"></span>"ProcessUnderTest"  
对于运行时分析很有用。 例如，如果测试测试"Explorer.exe"，然后运行雷达图 （运行时分析工具） 对该过程。

<span id="_Feature_"></span><span id="_feature_"></span><span id="_FEATURE_"></span>"Feature"  
将分类到特定功能或技术测试标识符。 这应视为 'cookie' 标识符谁具有的解释是到其定义的团队。

## <a name="span-idreservedmetadataspanspan-idreservedmetadataspanspan-idreservedmetadataspanreserved-metadata"></a><span id="_Reserved__Metadata"></span><span id="_reserved__metadata"></span><span id="_RESERVED__METADATA"></span>保留元数据


可能使用的以下元数据在将来-请不要使用它。

-   “用户”
-   IntegrityLevel
-   Timeout
-   HostType

 

 





