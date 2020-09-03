---
title: 静态驱动程序验证程序命令 (MSBuild)
description: 用于静态驱动程序验证程序的命令
ms.assetid: F0663631-AD7B-4BFE-8E07-7BB2FFC72911
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d23fb8362fc650a7a6186381ab476e7ecf98b119
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385067"
---
#  <a name="static-driver-verifier-commands-msbuild"></a>静态驱动程序验证程序命令 (MSBuild)


你可以通过安装 Windows 驱动程序工具包 (WDK) 或通过运行企业 Windows 驱动程序工具包 (EWDK) ，在 **Visual Studio 命令提示符** 窗口中运行静态驱动程序验证器 (SDV) 。 导航到存储驱动程序的项目文件或库的项目文件的目录。 参数可以在命令行上以任意顺序出现。

**注意**  SDV 在安装 WDK 时集成到 Visual Studio 中，也可以通过 "驱动程序" 菜单从 IDE 中运行。 

```
msbuild /t:sdv /p:Inputs="Parameters" ProjectFile /p:Configuration=configuration /p:Platform=platform     
```

您必须选择一个发布配置 (例如， **/p： configuration = "Windows 7 Release"**) 。 有关支持的版本配置的列表，请参阅 [构建驱动程序](../develop/building-a-driver.md)。 对于 x86) 或**x64** (，平台可以是**win32** (例如， **/p： Platform = Win32**) 。

**注意**  务必检查计算机的电源管理计划，以确保在分析期间计算机不会进入睡眠状态。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


### <span id="parameters"></span><span id="PARAMETERS"></span>

<span id="_scan"></span><span id="_SCAN"></span>/**检测**  
扫描驱动程序的函数角色类型声明的源代码。 有关如何声明驱动程序提供的回调函数和调度例程的信息，请参阅 [使用函数角色类型声明](using-function-role-type-declarations.md)。 在此扫描过程中，SDV 将尝试检测到需要验证驱动程序的驱动程序入口点。 它将扫描结果记录在 [Sdv](sdv-map-h.md)中，它是在驱动程序的项目目录中创建的文件。

有关详细信息，请参阅 [准备您的源代码](using-static-driver-verifier-to-find-defects-in-drivers.md#preparing_your_source_code)。

<span id="________check_Rule____Rule_..._"></span><span id="________check_rule____rule_..._"></span><span id="________CHECK_RULE____RULE_..._"></span>**/check：**<em>规则</em>  |  *规则*,.。。  
使用指定的规则 (s) 启动验证。 您可以通过用逗号分隔每个规则来指定多个规则。 运行 **/check：** 命令并指定驱动程序的 Visual Studio 项目文件 (\* . .vcxproj) 。

*规则* 是一种 [规则](static-driver-verifier-rule.md) 的名称或规则名称模式，其中包含 (\*) 表示一个或多个字符的通配符。 当单独使用时，通配符 (\*) 表示所有规则。

<span id="________check_rulelist.sdv______"></span><span id="________CHECK_RULELIST.SDV______"></span>**/check：*RuleList*. sdv**   
使用指定规则列表文件中的规则启动验证。 只能列出一个带有此参数的文件。 在规则列表文件中，每一行都可以是一个规则的名称，也可以是 () 的通配符 \* ，这表示所有 SDV 规则。  运行 **/check：*RuleList*. sdv** 命令，并指定驱动程序的 Visual Studio 项目文件 (\* .vcxproj) 。

<em>RuleList</em>**. sdv** 是 [规则列表文件](static-driver-verifier-rule-list-file.md)的完全限定路径和文件名。 文件必须具有扩展名 **sdv** 。 除非文件位于本地目录中，否则路径是必需的。 如果路径或文件名包含空格，则必须将 RuleList 括起来<em>。</em>用引号引起来的**sdv** 。

如果在不指定规则的情况下指定 **/check：** 选项，则会使用驱动程序模型的默认规则集运行 SDV。

<span id="________lib______"></span><span id="________LIB______"></span>**/lib**   
处理当前目录中的库。 SDV 调用 MSBuild.exe 来编译和生成用于外部使用的库，并生成在驱动程序验证中包含库所需的文件。

在验证需要库的驱动程序之前，请使用此参数。 运行 **msbuild/t： sdv/p： .vcxproj = "/lib"** 命令并为库指定 Visual Studio 项目文件 (\* .) 。

有关 **/lib** 参数的使用和效果的详细信息，请参阅 [静态驱动程序验证程序中的库处理](library-processing-in-static-driver-verifier.md)。

<span id="________view______"></span><span id="________VIEW______"></span>**/view**   
打开 "静态驱动程序验证程序"。 运行 **/view** 命令，并指定驱动程序的 Visual Studio 项目文件 (\* . .vcxproj) 。

验证完成后，结果会立即可用，并保持可用，直到你使用 **/clean** 命令从驱动程序的项目目录中删除 SDV 文件。

<span id="________clean______"></span><span id="________CLEAN______"></span>**/clean**   
从目录中删除 SDV 文件。 由于这些文件用于生成静态驱动程序验证程序报告显示，因此 **/clean** 命令还会删除该验证的报告。

运行 **/clean** 命令，并为驱动程序或库指定 Visual Studio 项目文件 (\* . .vcxproj) 。 该命令仅删除指定项目的 SDV 文件。

在每次验证之前，对驱动程序项目运行 **/clean** 命令。

库文件过期时，运行库的 **/clean** 命令，例如当库代码发生更改时。

如果 Sdv 标志设置为 true，则 **/clean** 命令不会删除 Sdv 文件，因为的标志设置为 true)  (已批准。 然后，SDV 可以使用此文件进行未来验证。

<span id="_______________"></span> **/?**   
显示 SDV 命令的用法。 使用此参数的命令不必在生成环境窗口中运行。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

正在运行 **msbuild/t：/sdv p：/输入 =/？** 如果没有参数，则显示 SDV 命令的用法。

**/Clean**命令删除 SDV 用于创建用于验证的静态驱动程序验证程序报告显示的文件。 运行此命令后，将不再提供用于验证的静态驱动程序验证程序报告显示。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

<span id="To_run_SDV_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="to_run_sdv_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="TO_RUN_SDV_USING_ALL_RULES_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_FOR_THE_MYDRIVER_PROJECT_"></span>若要在 mydriver 项目的本地目录中使用驱动程序文件上的所有规则运行 SDV，请执行以下操作：  
```
msbuild /t:sdv /p:Inputs="/check:*" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_run_SDV_using_the_CancelSpinLock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="to_run_sdv_using_the_cancelspinlock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="TO_RUN_SDV_USING_THE_CANCELSPINLOCK_RULE_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_"></span>若要在本地目录中的驱动程序文件上使用 [CancelSpinLock](./wdm-cancelspinlock.md) 规则运行 SDV，请执行以下操作：  
```
msbuild /t:sdv /p:Inputs="/check:CancelSpinLock" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_using_the_rule_that_is_specified_in_the_rules1.sdv_rule_list_file_in_the_d__sdv_directory_"></span><span id="TO_RUN_SDV_USING_THE_RULE_THAT_IS_SPECIFIED_IN_THE_RULES1.SDV_RULE_LIST_FILE_IN_THE_D__SDV_DIRECTORY_"></span>若要使用 D： SDV 目录中 Rules1 SDV 规则列表文件中指定的规则运行 SDV，请 \\ 执行以下操作：  
```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\Rules1.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_again__this_time_using_the__clean_option."></span><span id="TO_RUN_SDV_AGAIN__THIS_TIME_USING_THE__CLEAN_OPTION."></span>若要再次运行 SDV，请使用/clean 选项。  
```
msbuild /t:sdv /p:Inputs="/clean" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_display_Static_Driver_Verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="to_display_static_driver_verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="TO_DISPLAY_STATIC_DRIVER_VERIFIER__SO_THAT_YOU_CAN_VIEW_THE_RESULTS_FOR_THE_MOST_RECENT_VERIFICATION_OF_THE_DRIVER_IN_THE_LOCAL_DIRECTORY_"></span>若要显示静态驱动程序验证程序，以便可以查看本地目录中驱动程序的最新验证结果：  
```
msbuild /t:sdv /p:Inputs="/view" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用静态驱动程序验证程序查找 Windows 驱动程序中的缺陷](using-static-driver-verifier-to-find-defects-in-drivers.md)

 

