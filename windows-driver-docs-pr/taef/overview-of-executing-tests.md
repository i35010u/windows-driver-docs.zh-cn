---
title: 执行测试概述
description: 执行测试概述
ms.assetid: 3D58D074-DC06-4b01-9EB5-7A17E69D6935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3b6196e70854fc3a97653834bfecc154557edf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577469"
---
# <a name="overview-of-executing-tests"></a>执行测试概述


执行使用 TAEF 测试很简单;只需指定与命令"TE 测试文件。EXE"。 例如，若要运行所有测试中"CPP。Basic.Examples.dll"测试文件中，你可以运行;

``` syntax
TE.exe CPP.Basic.Examples.dll
```

可以指定多个测试文件，即使它们包含以不同方式标记的测试。 例如，以下命令将运行所有测试，在"CPP。Basic.Examples.dll"和"CSharp.Basic.Examples.dll"文件，即使它们以不同的语言;

``` syntax
TE.exe CPP.Basic.Examples.dll CSharp.Basic.Examples.dll
```

用于选择要执行的文件，您还可以使用通配符：

``` syntax
TE.exe *.Examples.dll
```

并且还可以指定相对路径：

``` syntax
TE.exe Examples\*
```

如果不包含任何测试的命令提示符处指定一个文件，则测试将报告一条错误消息。

## <a name="span-idorderofexecutionspanspan-idorderofexecutionspanspan-idorderofexecutionspanorder-of-execution"></a><span id="Order_of_Execution"></span><span id="order_of_execution"></span><span id="ORDER_OF_EXECUTION"></span>执行顺序


在命令提示符下指定的测试文件将以指定它们的顺序处理。

## <a name="span-idoutofprocessexecutionspanspan-idoutofprocessexecutionspanspan-idoutofprocessexecutionspanout-of-process-execution"></a><span id="OutOfProcessExecution"></span><span id="outofprocessexecution"></span><span id="OUTOFPROCESSEXECUTION"></span>从过程执行


默认情况下 TAEF 执行测试进程外-它使用"TE。若要运行测试的 ProcessHost.exe"过程。 这样，测试是相互独立的-阻止之前测试受影响的测试。 如果你想要在"TE.exe"进程中执行测试，则可以指定 **"/ inproc"** TE.exe 的选项。

## <a name="span-idselectingtestsspanspan-idselectingtestsspanspan-idselectingtestsspanselecting-tests"></a><span id="Selecting_Tests"></span><span id="selecting_tests"></span><span id="SELECTING_TESTS"></span>选择测试


可以使用选择特定测试 **"/ 选择"** 选项，并指定选择查询。 [选择](selection.md)页说明如何使用所选内容查询来选择要执行的特定测试。 如果你想要选择基于仅测试的名称，则可以使用 **"/name"** 选项。 请参阅所选内容页面了解详细信息。

## <a name="span-idspecifyingpartofcommandasenvironmentvariabletecmdspanspan-idspecifyingpartofcommandasenvironmentvariabletecmdspanspan-idspecifyingpartofcommandasenvironmentvariabletecmdspanspecifying-part-of-command-as-environment-variable-tecmd"></a><span id="Specifying_part_of_command_as_environment_variable__te_cmd"></span><span id="specifying_part_of_command_as_environment_variable__te_cmd"></span><span id="SPECIFYING_PART_OF_COMMAND_AS_ENVIRONMENT_VARIABLE__TE_CMD"></span>为环境变量指定命令的一部分： **te\_cmd**


如果某些 te.exe 命令的选项将始终保持相同，则可以利用环境变量**te\_cmd**。 任何 te\_cmd 设置为将追加到适用于 te.exe 执行的命令。 使用"*设置 te\_cmd = / 列表*"，您始终会看到在命令提示符处指定的二进制文件与执行测试的列表。

## <a name="span-idlistingtestsspanspan-idlistingtestsspanspan-idlistingtestsspanlisting-tests"></a><span id="Listing_Tests"></span><span id="listing_tests"></span><span id="LISTING_TESTS"></span>列出测试


指定 **"/ 列出"** 命令以及测试文件的选项将列出的类的名称，并在控制台上的测试文件中测试方法。 请注意，这将仅列出二进制、 类和测试方法名称，为每个指定的二进制文件，并不执行它们。 如果想要列出更多详细信息，例如设置和清理方法、 元数据或在每个级别指定的属性，并且对于数据驱动的测试中，数据提供，使用 **"/ listproperties"** 改为命令选项。

## <a name="span-idtestresultsspanspan-idtestresultsspanspan-idtestresultsspantest-results"></a><span id="Test_Results"></span><span id="test_results"></span><span id="TEST_RESULTS"></span>测试结果


对于任何通用测试用例的测试结果取决于是否进行成功或失败的验证调用。 您可以找到有关 Api 可和其他详细信息[验证](verify.md)。 如果在测试期间不进行任何验证调用时，测试结果将默认为"通过"随附 TAEF 中的日志订阅者。 您可以选择指定 **"DefaultTestResult"** 显式创作测试时。 请参阅[创作测试](authoring-tests.md)的更多详细信息。

## <a name="span-idhelp-commandoptionsspanspan-idhelp-commandoptionsspanspan-idhelp-commandoptionsspanhelp---command-options"></a><span id="Help_-_Command_Options"></span><span id="help_-_command_options"></span><span id="HELP_-_COMMAND_OPTIONS"></span>帮助-命令选项


可以通过指定查找所有可用的命令选项的 explantions **"/？"** TE.exe 选项。 有关扩展的说明，请参阅[Te.exe 命令选项](te-exe-command-line-parameters.md)。

 

 





