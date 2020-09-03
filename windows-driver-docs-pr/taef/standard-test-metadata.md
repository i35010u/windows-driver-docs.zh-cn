---
title: 标准测试元数据
description: 标准测试元数据
ms.assetid: A95FC176-B3A1-4bbf-833E-411CDE73C571
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c727dafc2b68c34c07b7d40466df6c805dd8d734
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403518"
---
# <a name="standard-test-metadata"></a>标准测试元数据


以下测试 "标记" 元数据是可应用于 TAEF 测试的标准元数据。

## <a name="span-idimplicit_metadataspanspan-idimplicit_metadataspanspan-idimplicit_metadataspanimplicit-metadata"></a><span id="Implicit_Metadata"></span><span id="implicit_metadata"></span><span id="IMPLICIT_METADATA"></span>隐式元数据


某些元数据会自动从测试标记中推断出来：

-   "名称"-测试的完全限定名称。
-   "体系结构"-DLL 的处理器结构。 此值将是 "x86"、"x64" 或 "arm" 之一。
-   "Testfile.txt"-中描述了测试的 DLL 文件。

## <a name="span-idselection_metadataspanspan-idselection_metadataspanspan-idselection_metadataspanselection-metadata"></a><span id="Selection_Metadata"></span><span id="selection_metadata"></span><span id="SELECTION_METADATA"></span>选择元数据


选择的元数据只是 "首选" 的元数据部分，允许团队提供标准，使他们能够更好地使用另一个测试。 不需要元数据的元数据会增加自动化的成本，所有元数据应是可选的，或者应启用 "选择加入" 行为。

在某些情况下，可以为元数据值指定多个值，在这种情况下，应使用以分号分隔的列表，并使用 "包含" 样式选择查询来测试。 例如，如果 "所有者" 元数据需要两个值，则应将其设置为 "某人;SomeoneElse". 用于选择仅由某人拥有的测试的查询为：

``` syntax
te Wex.Common.Tests.dll /select:@Owner='Someone'
```

然而，下面的查询将选择由某人拥有或共同拥有的测试：

``` syntax
te Wex.Common.Tests.dll /select:@Owner='*Someone*'
```

你可以定义自己的元数据以在你自己的公司中使用。 建议遵循以下建议。 .

## <a name="span-id_you_should__metadataspanspan-id_you_should__metadataspanspan-id_you_should__metadataspanyou-should-metadata"></a><span id="_You_should...__Metadata"></span><span id="_you_should...__metadata"></span><span id="_YOU_SHOULD...__METADATA"></span>"您应该 ..."新元


这些元数据属性为建议，具有明确的含义。 根据需要使用这些元数据属性：

<span id="_ActivationContext_"></span><span id="_activationcontext_"></span><span id="_ACTIVATIONCONTEXT_"></span>ActivationContext  
从系统中的各种并行程序集指定二进制文件的特定版本。 有关详细信息，请参阅 [激活上下文](activation-context.md) 。

<span id="_BinaryUnderTest_"></span><span id="_binaryundertest_"></span><span id="_BINARYUNDERTEST_"></span>"BinaryUnderTest"  
给定测试是单元测试的二进制 \[ 文件 \] 。 这允许开发人员快速运行验证给定 DLL 的所有单元测试。

<span id="_DefaultTestResult_"></span><span id="_defaulttestresult_"></span><span id="_DEFAULTTESTRESULT_"></span>"DefaultTestResult"  
重写给定测试的 "通过" 的默认测试结果。 如果测试通过，则记录的结果将是默认的测试结果。 可能的值为 "已通过"、"已失败"、"NotRun"、"已阻止" 和 "已跳过"。

<span id="_DeploymentItem_"></span><span id="_deploymentitem_"></span><span id="_DEPLOYMENTITEM_"></span>[DeploymentItem](deploymentitem-metadata.md)  
将文件和文件夹标识为测试依赖项。

<span id="_Description_"></span><span id="_description_"></span><span id="_DESCRIPTION_"></span>2008  
对测试任务的简短说明。

<span id="_DpiAware_"></span><span id="_dpiaware_"></span><span id="_DPIAWARE_"></span>"DpiAware"  
设置为 "true" 时，TAEF 会在标记为 DPI 感知的进程中运行测试，请参阅 [高 DPI](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)。

<span id="_ExecutionGroup_"></span><span id="_executiongroup_"></span><span id="_EXECUTIONGROUP_"></span>"ExecutionGroup"  
类中的一组连续测试，这些测试需要按顺序运行，并且如果执行组中前面的测试未运行或失败，则会被阻止。 有关详细信息，请参阅 [执行组](execution-groups.md) 。

<span id="_Ignore_"></span><span id="_ignore_"></span><span id="_IGNORE_"></span>暂且  
在执行或通过 TAEF 列出时，将跳过具有 "Ignore" 元数据设置为 "true" 的测试类或测试方法。 若要重写此行为，并运行或列出包含 "Ignore" 元数据的所有测试，请将 **/runIgnoredTests** 指定为命令行参数。

<span id="_IsolationLevel_"></span><span id="_isolationlevel_"></span><span id="_ISOLATIONLEVEL_"></span>IsolationLevel  
指定执行 TAEF 测试时要使用的最低隔离级别。 有关更多详细信息，请参阅 [测试隔离](test-isolation.md) 。

<span id="_Parallel_"></span><span id="_parallel_"></span><span id="_PARALLEL_"></span>[并行](parallel.md)  
并行执行多个处理器上的测试。 有关更多详细信息，请参阅 [并行](parallel.md)。

<span id="_Priority_"></span><span id="_priority_"></span><span id="_PRIORITY_"></span>大事  
整数形式的测试优先级，较小的优先级。

<span id="_RebootPossible_"></span><span id="_rebootpossible_"></span><span id="_REBOOTPOSSIBLE_"></span>["RebootPossible"](reboot.md)  
如果设置为 true，则允许使用重新启动 Api 来请求 TAEF 执行计算机重启或通知 TAEF 即将开始的测试启动的重新启动。

<span id="_RunAs_"></span><span id="_runas_"></span><span id="_RUNAS_"></span>方式  
指定应在其中运行关注的测试的上下文。 有关详细信息，请参阅 [RunAs 执行](runas.md) 。

<span id="_RunFixtureAs_"></span><span id="_runfixtureas_"></span><span id="_RUNFIXTUREAS_"></span>["RunFixtureAs"](runfixtureas.md)  
指定应在其中运行考虑的测试装置的上下文。 有关详细信息，请参阅 [RunFixtureAs](runfixtureas.md) 。

<span id="_TestClassification_Scope_"></span><span id="_testclassification_scope_"></span><span id="_TESTCLASSIFICATION_SCOPE_"></span>"TestClassification： Scope"  
测试分类 "范围" 标识用于验证 Windows 中发生的 "工程处理事件" 的测试宣传品。

<span id="_TestClassification_Type_"></span><span id="_testclassification_type_"></span><span id="_TESTCLASSIFICATION_TYPE_"></span>"TestClassification： Type"  
测试分类 "Type" 标识需要区分的测试类型。

<span id="_TestClassification_"></span><span id="_testclassification_"></span><span id="_TESTCLASSIFICATION_"></span>"TestClassification"  
使用属性值 "Unit： WUTG" 指示符合 Windows 单元测试准则 (WUTG) 的单元测试。 使用属性值 "Unit： WUTG： ChexGate" 指示符合 Windows 单元测试准则 (WUTG) 的单元测试，并应在 Chex 方案的封闭阶段中运行 (故障阻止提交) 。

<span id="_TestTimeout_"></span><span id="_testtimeout_"></span><span id="_TESTTIMEOUT_"></span>"TestTimeout"  
指定给定测试或安装/清理方法可以执行的最大时间量。 有关详细信息，请参阅[超时](taef-timeouts.md)。

<span id="_ThreadingModel_"></span><span id="_threadingmodel_"></span><span id="_THREADINGMODEL_"></span>ThreadingModel  
测试使用的预先配置的 COM 线程处理模型。 有关详细信息，请参阅 [配置线程模型](threading-models.md) 。

与数据驱动的测试相关：

<span id="_DataSource_"></span><span id="_datasource_"></span><span id="_DATASOURCE_"></span>DataSource  
指定 [数据驱动测试](data-driven-testing.md)的数据的主要来源。

<span id="_TableId_"></span><span id="_tableid_"></span><span id="_TABLEID_"></span>TableId  
指定 [基于表的数据驱动测试](table-data-source.md)时，与 "DataSource" 分隔的表的名称或 Id。

<span id="_Pict_Timeout___and_deprecated__PictTimeout__"></span><span id="_pict_timeout___and_deprecated__picttimeout__"></span><span id="_PICT_TIMEOUT___AND_DEPRECATED__PICTTIMEOUT__"></span>"Pict： Timeout" (和弃用的 "PictTimeout" )   
覆盖在 [基于 PICT 的数据驱动测试](pict-data-source.md)时，PICT.exe 允许用于处理用户指定的模型文件的默认超时值（以秒为单位）。

<span id="_Pict_SeedingFile___and_deprecated__Seed__"></span><span id="_pict_seedingfile___and_deprecated__seed__"></span><span id="_PICT_SEEDINGFILE___AND_DEPRECATED__SEED__"></span>"Pict： SeedingFile" (和弃用的 "种子" )   
指定 seed 文件的相对位置，与 [基于 PICT 的数据驱动测试的数据](pict-data-source.md)源不同。

<span id="_Pict_Order_"></span><span id="_pict_order_"></span><span id="_PICT_ORDER_"></span>"Pict： Order"  
指定在 [基于 PICT 的数据驱动测试](pict-data-source.md)中调用时 PICT.exe 的/o 参数的值。

<span id="_Pict_ValueSeparator_"></span><span id="_pict_valueseparator_"></span><span id="_PICT_VALUESEPARATOR_"></span>"Pict： ValueSeparator"  
指定在 [基于 PICT 的数据驱动测试](pict-data-source.md)中调用时 PICT.exe/d 参数的值。

<span id="_Pict_AliasSeparator_"></span><span id="_pict_aliasseparator_"></span><span id="_PICT_ALIASSEPARATOR_"></span>"Pict： AliasSeparator"  
指定在 [基于 PICT 的数据驱动测试](pict-data-source.md)中调用 PICT.exe 时/a 参数的值。

<span id="_Pict_NegativeValuePrefix_"></span><span id="_pict_negativevalueprefix_"></span><span id="_PICT_NEGATIVEVALUEPREFIX_"></span>"Pict： NegativeValuePrefix"  
指定在 [基于 PICT 的数据驱动测试](pict-data-source.md)中调用时 PICT.exe 的/n 参数的值。

<span id="_Pict_Random_"></span><span id="_pict_random_"></span><span id="_PICT_RANDOM_"></span>"Pict：随机"  
指定在调用 [基于 PICT 的数据驱动测试](pict-data-source.md)PICT.exe 时是否应使用随机性。 如果为 true，则 TAEF 将记录所使用的随机种子。

<span id="_Pict_RandomSeed_"></span><span id="_pict_randomseed_"></span><span id="_PICT_RANDOMSEED_"></span>"Pict： RandomSeed"  
指定在 [基于 PICT 的数据驱动测试](pict-data-source.md)中调用时 PICT.exe 的/r 参数的值。 设置此选项会将 "Pict： Random" 的默认值从 false 更改为 true。

<span id="_Pict_CaseSensitive_"></span><span id="_pict_casesensitive_"></span><span id="_PICT_CASESENSITIVE_"></span>"Pict： CaseSensitive"  
指定在 [基于 PICT 的数据驱动测试](pict-data-source.md)中调用/c 参数时，是否应将其用于 PICT.exe。

支持设备相关：

<span id="_TestResourceDependent_"></span><span id="_testresourcedependent_"></span><span id="_TESTRESOURCEDEPENDENT_"></span>"TestResourceDependent"  
指定当前范围中的测试依赖于 BuildResourceList ( ... ) 收集的资源上的 TestResource 和函数。有关详细信息，请参阅 [设备支持](device-support.md) 。

<span id="_ResourceSelection_"></span><span id="_resourceselection_"></span><span id="_RESOURCESELECTION_"></span>"ResourceSelection"  
指定查询以匹配由 BuildResourceList ( 收集的 TestResources （与相关测试相关 ) 。 有关详细信息，请参阅 [设备支持](device-support.md) 。

## <a name="span-id_you_can__metadataspanspan-id_you_can__metadataspanspan-id_you_can__metadataspanyou-can-metadata"></a><span id="_You_can...__Metadata"></span><span id="_you_can...__metadata"></span><span id="_YOU_CAN...__METADATA"></span>"您可以 ..."新元


可以使用这些元数据属性，但不能保证它们的解释;团队可以在需要时使用它们。

<span id="_Owner_"></span><span id="_owner_"></span><span id="_OWNER_"></span>Owner  
测试所有者的别名。

<span id="_ProcessUnderTest_"></span><span id="_processundertest_"></span><span id="_PROCESSUNDERTEST_"></span>"ProcessUnderTest"  
适用于运行时分析。 例如，如果测试正在测试 "Explorer.exe"，则 (运行时分析工具) 执行该过程。

<span id="_Feature_"></span><span id="_feature_"></span><span id="_FEATURE_"></span>具有  
将测试分类为特定功能或技术的标识符。 这应被视为 "cookie" 标识符，其解释已向下的团队提供。

## <a name="span-id_reserved__metadataspanspan-id_reserved__metadataspanspan-id_reserved__metadataspanreserved-metadata"></a><span id="_Reserved__Metadata"></span><span id="_reserved__metadata"></span><span id="_RESERVED__METADATA"></span>"Reserved" 元数据


将来可能会使用以下元数据-请不要使用。

-   用户
-   IntegrityLevel
-   超时
-   HostType

 

