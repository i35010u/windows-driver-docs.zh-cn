---
ms.assetid: 388C0D27-F3B9-4EF0-A03C-B58F38F2EFD6
title: 驱动程序项目的消息编译器属性
description: 设置消息编译器 (MC.exe) 工具的属性。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5cbea73bb79d260dc703c226a5898c2784ecf5
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364257"
---
# <a name="message-compiler-properties-for-driver-projects"></a>驱动程序项目的消息编译器属性

设置[**消息编译器 (MC.exe)** ](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-) 工具的属性。 编译器将生成消息资源文件，你可以将其添加到项目中。

例如，如果你使用 [Windows 事件跟踪 (ETW)](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-) 内核模式 API 来为内核模式驱动程序添加事件跟踪，则可使用消息编译器来创建一个包含事件提供程序、事件属性、通道和事件的定义的头文件。 你必须在源代码中包括此头文件。 消息编译器将创建一个资源编译器脚本 (\*.rc)，你可以将其添加到项目文件中。

## <a name="span-idsetting_message_compiler_properties_for_driver_projectsspanspan-idsetting_message_compiler_properties_for_driver_projectsspanspan-idsetting_message_compiler_properties_for_driver_projectsspansetting-message-compiler-properties-for-driver-projects"></a><span id="Setting_Message_Compiler_properties_for_driver_projects"></span><span id="setting_message_compiler_properties_for_driver_projects"></span><span id="SETTING_MESSAGE_COMPILER_PROPERTIES_FOR_DRIVER_PROJECTS"></span>设置驱动程序项目的消息编译器属性


1.  打开驱动程序项目的属性页。 在“解决方案资源管理器”  中右键单击驱动程序项目，并选择“属性”  。
2.  在驱动程序项目的属性页中，单击“配置属性”  ，然后单击“消息编译器”  。
3.  设置项目属性。

如果你将消息文本文件 (.mc) 或清单 (.man) 添加到解决方案，则此属性页可用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Additional_Options"></span><span id="additional_options"></span><span id="ADDITIONAL_OPTIONS"></span><strong>其他选项</strong></p></td>
<td align="left"><p>指定要传递至<a href="https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-" data-raw-source="[&lt;strong&gt;Message Compiler (MC.exe)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)"><strong>消息编译器 (MC.exe)</strong></a> 工具的其他选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Ansi_Input_File"></span><span id="ansi_input_file"></span><span id="ANSI_INPUT_FILE"></span><strong>Ansi 输入文件</strong></p></td>
<td align="left"><p>指定输入文件包含 ANSI 内容（这是默认设置）。 (<strong>-a</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Ansi_Message_In_Bin_File"></span><span id="ansi_message_in_bin_file"></span><span id="ANSI_MESSAGE_IN_BIN_FILE"></span><strong>Bin 文件中的 Ansi 消息</strong></p></td>
<td align="left"><p>指定输出 .bin 文件中的消息应该为 ANSI。 (<strong>-A</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Baseline_Path"></span><span id="baseline_path"></span><span id="BASELINE_PATH"></span><strong>基线路径</strong></p></td>
<td align="left"><p>此路径必须指向包含基线操作创建的 .BIN 文件的文件夹。 (<strong>-t</strong> <目录>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Baseline_Resource_Path"></span><span id="baseline_resource_path"></span><span id="BASELINE_RESOURCE_PATH"></span><strong>基线资源路径</strong></p></td>
<td align="left"><p>包含基线清单文件的文件夹。 (<strong>-s</strong> <目录>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Debug_Output_Path"></span><span id="debug_output_path"></span><span id="DEBUG_OUTPUT_PATH"></span><strong>调试输出路径</strong></p></td>
<td align="left"><p>用于放置 .dbg C 包含文件的路径。 (<strong>-x</strong> <路径>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_Callout_Macro"></span><span id="enable_callout_macro"></span><span id="ENABLE_CALLOUT_MACRO"></span><strong>启用标注宏</strong></p></td>
<td align="left"><p>添加标注宏，以便在日志记录时调用用户代码。 不适用于 C#，已忽略。 (<strong>-co</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Debug_Output_Path"></span><span id="enable_debug_output_path"></span><span id="ENABLE_DEBUG_OUTPUT_PATH"></span><strong>启用调试输出路径</strong></p></td>
<td align="left"><p>允许编译器放置由<strong>调试输出路径</strong>属性指定的 .dbg C 包含文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="File_extension_for_the_generated_header"></span><span id="file_extension_for_the_generated_header"></span><span id="FILE_EXTENSION_FOR_THE_GENERATED_HEADER"></span><strong>生成的头文件的文件扩展名</strong></p></td>
<td align="left"><p>指定生成的头文件的扩展名。 (<strong>-e</strong> <扩展名>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_Baseline_Resource"></span><span id="generate_baseline_resource"></span><span id="GENERATE_BASELINE_RESOURCE"></span><strong>生成基线资源</strong></p></td>
<td align="left"><p>创建检测基线。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_C___managed__logging_class"></span><span id="generate_c___managed__logging_class"></span><span id="GENERATE_C___MANAGED__LOGGING_CLASS"></span><strong>生成 C#（托管）日志记录类</strong></p></td>
<td align="left"><p>生成一个 C#（托管）日志记录类，你可以通过调用其中包含的方法来将事件记录到清单中。 (<strong>-cs</strong> <命名空间>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_header_file_for_containing_counter_names_and_GUIDs"></span><span id="generate_header_file_for_containing_counter_names_and_guids"></span><span id="GENERATE_HEADER_FILE_FOR_CONTAINING_COUNTER_NAMES_AND_GUIDS"></span><strong>生成包含计数器名称和 GUID 的头文件</strong></p></td>
<td align="left"><p>使用此选项来指定你想要编译器在其中放置生成的头文件的文件夹。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_Kernel_Mode_Logging_Macros"></span><span id="generate_kernel_mode_logging_macros"></span><span id="GENERATE_KERNEL_MODE_LOGGING_MACROS"></span><strong>生成内核模式日志记录宏</strong></p></td>
<td align="left"><p>生成内核模式日志记录宏。 (<strong>-km</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_MOF_File"></span><span id="generate_mof_file"></span><span id="GENERATE_MOF_FILE"></span><strong>生成 MOF 文件</strong></p></td>
<td align="left"><p>为所有函数和生成的宏生成下级支持。 MOF 文件将通过清单生成。 MOF 文件将置于 <strong>-h</strong> 选项 (<strong>-mof</strong>) 指定的位置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_OLE2_Header"></span><span id="generate_ole2_header"></span><span id="GENERATE_OLE2_HEADER"></span><strong>生成 OLE2 头文件</strong></p></td>
<td align="left"><p>生成 OLE2 头文件。 (<strong>-o</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_static_C___managed__logging_class"></span><span id="generate_static_c___managed__logging_class"></span><span id="GENERATE_STATIC_C___MANAGED__LOGGING_CLASS"></span><strong>生成静态 C#（托管）日志记录类</strong></p></td>
<td align="left"><p>生成一个静态 C#（托管）日志记录类，你可以通过调用其中包含的方法来将事件记录到清单中。 (<strong>-css</strong> <命名空间>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_User_Mode_Logging_Macros"></span><span id="generate_user_mode_logging_macros"></span><span id="GENERATE_USER_MODE_LOGGING_MACROS"></span><strong>生成用户模式日志记录宏</strong></p></td>
<td align="left"><p>生成用户模式日志记录宏。 (<strong>-um</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generated_Files_Base_Name"></span><span id="generated_files_base_name"></span><span id="GENERATED_FILES_BASE_NAME"></span><strong>生成文件基名</strong></p></td>
<td align="left"><p>指定所有生成文件的基名。 (<strong>-z</strong> <基名>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generated_RC_and_Binary_Message_Files_Path"></span><span id="generated_rc_and_binary_message_files_path"></span><span id="GENERATED_RC_AND_BINARY_MESSAGE_FILES_PATH"></span><strong>生成 RC 和二进制消息文件路径</strong></p></td>
<td align="left"><p>指定生成的 RC 和二进制消息文件的路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Header_File_Path"></span><span id="header_file_path"></span><span id="HEADER_FILE_PATH"></span><strong>头文件路径</strong></p></td>
<td align="left"><p>指定生成的头文件的路径。 (<strong>-h</strong> <路径>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Maximum_Message_Length"></span><span id="maximum_message_length"></span><span id="MAXIMUM_MESSAGE_LENGTH"></span><strong>最大消息长度</strong></p></td>
<td align="left"><p>使用此参数来让编译器在任何消息超出字符长度时生成警告。 (<strong>-m</strong> <长度>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Prefix_Macro_Name"></span><span id="prefix_macro_name"></span><span id="PREFIX_MACRO_NAME"></span><strong>前缀宏名称</strong></p></td>
<td align="left"><p>使用此参数来覆盖编译器用于记录宏名称和方法名称的默认前缀。 (<strong>-p</strong> <前缀>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="RC_File_Path"></span><span id="rc_file_path"></span><span id="RC_FILE_PATH"></span><strong>RC 文件路径</strong></p></td>
<td align="left"><p>你想要编译器在其中放置生成的资源编译器脚本 (.rc file) 和生成的 .bin 文件的文件夹。 (<strong>-r</strong> <路径>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Remove_Characters_From_Symbolic_Name"></span><span id="remove_characters_from_symbolic_name"></span><span id="REMOVE_CHARACTERS_FROM_SYMBOLIC_NAME"></span><strong>从符号名称中删除字符</strong></p></td>
<td align="left"><p>使用此参数来从你为事件指定的符号名称开始删除字符。 (<strong>-P</strong> <前缀>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Set_Customer_Bit"></span><span id="set_customer_bit"></span><span id="SET_CUSTOMER_BIT"></span><strong>设置客户位</strong></p></td>
<td align="left"><p>在整个消息 ID 中设置客户位。 (<strong>-c</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Terminate_Message_With_Null"></span><span id="terminate_message_with_null"></span><span id="TERMINATE_MESSAGE_WITH_NULL"></span><strong>终止 NULL 消息</strong></p></td>
<td align="left"><p>终止消息表中为 NULL 的所有字符串。 (<strong>-n</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Unicode_Input_File"></span><span id="unicode_input_file"></span><span id="UNICODE_INPUT_FILE"></span><strong>Unicode 输入文件</strong></p></td>
<td align="left"><p>指定包含 Unicode 内容的输入文件。 (<strong>-u</strong>)</p>
<p>默认值为 ANSI。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Unicode_Message_In_Bin_File"></span><span id="unicode_message_in_bin_file"></span><span id="UNICODE_MESSAGE_IN_BIN_FILE"></span><strong>Bin 文件中的 Unicode 消息</strong></p></td>
<td align="left"><p>指定输出 .bin 文件中的消息为 Unicode。 (<strong>-U</strong>)</p>
<p>这是默认设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Use_Base_Name_Of_Input"></span><span id="use_base_name_of_input"></span><span id="USE_BASE_NAME_OF_INPUT"></span><strong>使用输入的基名</strong></p></td>
<td align="left"><p>使用此参数可让编译器将输入文件的基名用作输出 .bin 文件的名称。 (<strong>-b</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Use_Decimal_Values"></span><span id="use_decimal_values"></span><span id="USE_DECIMAL_VALUES"></span><strong>使用十进制值</strong></p></td>
<td align="left"><p>使用此参数即可在头文件的 Severity 和 Facility 常量中使用十进制值，而不是十六进制值。 (<strong>-d</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Validate_Against_Baseline_Resource"></span><span id="validate_against_baseline_resource"></span><span id="VALIDATE_AGAINST_BASELINE_RESOURCE"></span><strong>针对基线资源进行验证</strong></p></td>
<td align="left"><p>当你创建新版清单并想要针对你使用 <strong>-s</strong> 选项创建的基线检查其是否与应用程序兼容时，可以使用此参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verbose"></span><span id="verbose"></span><span id="VERBOSE"></span><strong>详细</strong></p></td>
<td align="left"><p>使用此选项来生成详细输出。 (<strong>-v</strong>)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [消息编译器 (MC.exe)](https://docs.microsoft.com/windows-hardware/drivers/devtest/message-compiler-task)
* [WDK 和 Visual Studio 生成环境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)消息编译器任务
* [Windows 事件跟踪 (ETW)](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)
 

 






