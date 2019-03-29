---
title: 静态驱动程序验证程序命令 (MSBuild)
description: 与 Static Driver Verifier 一起使用的命令
ms.assetid: F0663631-AD7B-4BFE-8E07-7BB2FFC72911
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8c956588adc855333659e8978ead5156ff09636
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565959"
---
#  <a name="static-driver-verifier-commands-msbuild"></a>静态驱动程序验证程序命令 (MSBuild)


您可以在运行 Static Driver Verifier (SDV) **Visual Studio 命令提示符**窗口中的，通过安装 Windows Driver Kit (WDK) 或通过运行企业 Windows 驱动程序工具包 (EWDK)。 导航到存储驱动程序的项目文件或库的项目文件的目录。 参数可以在命令行上的任何顺序出现。

**请注意**SDV 集成到 Visual Studio 在安装 WDK 时，也可以运行从 IDE 通过"驱动程序"菜单。 

```
msbuild /t:sdv /p:Inputs="Parameters" ProjectFile /p:Configuration=configuration /p:Platform=platform     
```

必须选择发布配置 (例如， **/p:Configuration ="Windows 7 Release"**)。 有关支持的发布配置的列表，请参阅[构建一个驱动程序](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)。 平台如何能够**Win32** （适用于 x86) 或**x64** (例如， **/p:Platform = Win32**)。

**请注意**请务必检查您的计算机的电源管理计划，以确保计算机不会进入睡眠状态在分析过程。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


### <span id="parameters"></span><span id="PARAMETERS"></span>

<span id="_scan"></span><span id="_SCAN"></span>/**scan**  
扫描函数角色类型声明的驱动程序的源代码。 有关如何声明驱动程序提供回调函数和调度例程的信息，请参阅[使用函数角色类型声明](using-function-role-type-declarations.md)。 此扫描期间 SDV 尝试检测它需要验证该驱动程序的驱动程序入口点。 记录中扫描的结果[Sdv map.h](sdv-map-h.md)，它的驱动程序的项目目录中创建的文件。

有关详细信息，请参阅[准备你的源代码](using-static-driver-verifier-to-find-defects-in-drivers.md#preparing_your_source_code)。

<span id="________check_Rule____Rule_..._"></span><span id="________check_rule____rule_..._"></span><span id="________CHECK_RULE____RULE_..._"></span> **/check:**<em>规则</em> | *规则*，...  
使用指定的规则启动验证。 可以用逗号分隔每个规则来指定多个规则。 运行 **/check:** 命令并指定驱动程序的 Visual Studio 项目文件 (\*.vcxproj)。

*规则*是其中一个的名称[规则](static-driver-verifier-rule.md)或包含通配符的规则名称模式 (\*) 来表示一个或多个字符。 单独使用通配符字符时，(\*) 表示所有规则。

<span id="________check_rulelist.sdv______"></span><span id="________CHECK_RULELIST.SDV______"></span> **/check:*RuleList*.sdv**   
使用指定的规则列表文件中的规则启动验证。 可以列出与此参数只能有一个文件。 在规则列表文件中，每一行可以是一个规则的名称，也可以是通配符 (\*)，它表示所有 SDV 规则。  运行 **/check:*RuleList*.sdv**命令并指定驱动程序的 Visual Studio 项目文件 (\*.vcxproj)。

<em>RuleList</em>**.sdv**的是完全限定的路径和文件名[规则列表文件](static-driver-verifier-rule-list-file.md)。 该文件必须具有 **.sdv**文件扩展名。 除非文件为本地目录中，路径是必需的。 如果路径或文件名称包含空格，必须将<em>RuleList。</em>**sdv**引号引起来。

如果指定 **/check:** 选项而无需指定规则，SDV 为驱动程序模型设置的默认规则使用运行。

<span id="________lib______"></span><span id="________LIB______"></span> **/lib**   
处理当前目录中的库。 SDV 调用 MSBuild.exe 编译和生成适用于外部使用的库，并生成它需要驱动程序验证中包含库的文件。

验证要求库的驱动程序之前使用此参数。 运行**msbuild /t:sdv /p:Inputs ="/ lib"** 命令并指定 Visual Studio 项目文件 (\*.vcxproj) 库。

有关使用和作用的详细信息 **/lib**参数，请参阅[库处理中 Static Driver Verifier](library-processing-in-static-driver-verifier.md)。

<span id="________view______"></span><span id="________VIEW______"></span> **/view**   
将打开的 Static Driver Verifier。 运行 **/视图**的命令并指定驱动程序的 Visual Studio 项目文件 (\*.vcxproj)。

结果一旦完成验证后，就可用并保持可用，则直到您使用 **/clean**命令以删除 SDV 文件从驱动程序的项目目录。

<span id="________clean______"></span><span id="________CLEAN______"></span> **/clean**   
从目录中删除 SDV 文件。 因为这些文件用于生成静态驱动程序验证工具报表视图、 **/clean**命令还会删除验证的报表。

运行 **/clean**命令并指定 Visual Studio 项目文件 (\*.vcxproj) 驱动程序或库。 此命令删除 SDV 文件仅为指定的项目。

运行 **/clean**命令之前每个验证驱动程序项目。

运行 **/clean**命令时的库文件已过时，例如当库代码的更改的库。

一个 **/clean**命令不会删除 Sdv map.h 文件中，如果已批准的标志设置为 Sdv map.h 文件中，则返回 true (已批准 = true)。 SDV 然后可以使用此文件进行验证。

<span id="_______________"></span> **/?**   
SDV 命令显示使用情况。 使用此参数的命令，无需在生成环境窗口中运行。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

运行**msbuild/t: / sdv p: / 输入 = /？** 不带参数显示的 SDV 命令的使用情况。

一个 **/clean**命令删除 SDV 使用来创建验证静态驱动程序验证工具报表显示的文件。 运行此命令后，验证的驱动程序验证程序的静态报表显示不再可用。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

<span id="To_run_SDV_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="to_run_sdv_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="TO_RUN_SDV_USING_ALL_RULES_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_FOR_THE_MYDRIVER_PROJECT_"></span>若要运行 SDV mydriver 项目的本地目录中的驱动程序文件上使用所有规则：  
```
msbuild /t:sdv /p:Inputs="/check:*" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_run_SDV_using_the_CancelSpinLock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="to_run_sdv_using_the_cancelspinlock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="TO_RUN_SDV_USING_THE_CANCELSPINLOCK_RULE_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_"></span>若要运行使用 SDV [CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478)上的本地目录中的驱动程序文件的规则：  
```
msbuild /t:sdv /p:Inputs="/check:CancelSpinLock" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_using_the_rule_that_is_specified_in_the_rules1.sdv_rule_list_file_in_the_d__sdv_directory_"></span><span id="TO_RUN_SDV_USING_THE_RULE_THAT_IS_SPECIFIED_IN_THE_RULES1.SDV_RULE_LIST_FILE_IN_THE_D__SDV_DIRECTORY_"></span>若要运行使用 d: Rules1.sdv 规则列表文件中指定的规则的 SDV\\SDV 目录：  
```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\Rules1.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_again__this_time_using_the__clean_option."></span><span id="TO_RUN_SDV_AGAIN__THIS_TIME_USING_THE__CLEAN_OPTION."></span>若要再次运行 SDV，这次使用的 / 清理选项。  
```
msbuild /t:sdv /p:Inputs="/clean" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_display_Static_Driver_Verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="to_display_static_driver_verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="TO_DISPLAY_STATIC_DRIVER_VERIFIER__SO_THAT_YOU_CAN_VIEW_THE_RESULTS_FOR_THE_MOST_RECENT_VERIFICATION_OF_THE_DRIVER_IN_THE_LOCAL_DIRECTORY_"></span>若要显示 Static Driver Verifier，以便可以在本地目录中查看最新的驱动程序验证的结果：  
```
msbuild /t:sdv /p:Inputs="/view" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 Static Driver Verifier Windows 驱动程序中查找缺陷](using-static-driver-verifier-to-find-defects-in-drivers.md)

 

 






