---
ms.assetid: 216E5337-0B05-4560-92AF-0D7AB90EAEEB
title: 驱动程序项目的计数器清单预处理器属性
description: 设置分析和验证计数器清单的 CTRPP 工具的属性。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e66c284106594c31d6499f929abb42f1129c5ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518280"
---
# <a name="counters-manifest-preprocessor-properties-for-driver-projects"></a>驱动程序项目的计数器清单预处理器属性

设置分析和验证计数器清单的 [CTRPP](https://msdn.microsoft.com/library/windows/desktop/aa372128) 工具的属性。 有关使用性能计数器的信息，请参阅[性能计数器](https://msdn.microsoft.com/Library/Windows/Desktop/aa373083)。 有关在内核模式 Windows 驱动程序中使用性能计数器的信息，请参阅[内核模式性能监视](https://msdn.microsoft.com/Library/Windows/Hardware/Ff548159)。

## <a name="span-idsettingthecountersmanifestpreprocessorpropertiesfordriverprojectsspanspan-idsettingthecountersmanifestpreprocessorpropertiesfordriverprojectsspanspan-idsettingthecountersmanifestpreprocessorpropertiesfordriverprojectsspansetting-the-counters-manifest-preprocessor-properties-for-driver-projects"></a><span id="Setting_the_Counters_Manifest_Preprocessor_properties_for_driver_projects"></span><span id="setting_the_counters_manifest_preprocessor_properties_for_driver_projects"></span><span id="SETTING_THE_COUNTERS_MANIFEST_PREPROCESSOR_PROPERTIES_FOR_DRIVER_PROJECTS"></span>设置驱动程序项目的计数器清单预处理器属性


1.  打开驱动程序项目的属性页。 在**解决方案资源管理器**中右键单击驱动程序项目，并选择“属性”。
2.  在驱动程序项目的属性页中，依次单击“配置属性”和“计数器清单预处理器属性”。
3.  设置项目属性。

如果你想要将此属性页添加到你的项目，以便可以在生成过程中运行 CTRPP 工具，请参阅 [WDK 和 Visual Studio 生成环境](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454286)和 [Ctrpp 任务](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454206)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Add_Prefix"></span><span id="add_prefix"></span><span id="ADD_PREFIX"></span>添加前缀</p></td>
<td align="left"><p>指定在生成的头文件中定义的全局变量和函数将使用的前缀（与 <strong>-prefix</strong> 命令选项相同）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Additional_Options"></span><span id="additional_options"></span><span id="ADDITIONAL_OPTIONS"></span>其他选项</p></td>
<td align="left"><p>向 <a href="https://msdn.microsoft.com/Library/Windows/Desktop/aa372128" data-raw-source="[&lt;strong&gt;CTRPP&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Desktop/aa372128)"><strong>CTRPP</strong></a> 工具指定其他选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Backward_Compatibility"></span><span id="backward_compatibility"></span><span id="BACKWARD_COMPATIBILITY"></span>向后兼容</p></td>
<td align="left"><p>生成与 Windows 7 之前的 Windows 版本兼容的二进制形式的代码（与 <strong>-backcompat</strong> 命令选项相同）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Legacy"></span><span id="enable_legacy"></span><span id="ENABLE_LEGACY"></span>启用旧版</p></td>
<td align="left"><p>还原为使用 Windows Vista 代码模板生成代码。 此选项会让 <a href="https://msdn.microsoft.com/Library/Windows/Desktop/aa372128" data-raw-source="[&lt;strong&gt;CTRPP&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Desktop/aa372128)"><strong>CTRPP</strong></a> 生成四个输出文件：两个头文件（.h、_r.h）、一个资源文件 (.rc) 和一个源代码文件 (c)。 (<strong>-legacy</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_header_file_for_containing_counter_names_and_GUIDs"></span><span id="generate_header_file_for_containing_counter_names_and_guids"></span><span id="GENERATE_HEADER_FILE_FOR_CONTAINING_COUNTER_NAMES_AND_GUIDS"></span>生成包含计数器名称和 GUID 的头文件</p></td>
<td align="left"><p>创建将符号分配给清单中的每个计数器集的计数器集名称和 GUID 的头文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_header_file_for_provider"></span><span id="generate_header_file_for_provider"></span><span id="GENERATE_HEADER_FILE_FOR_PROVIDER"></span>生成提供程序的头文件</p></td>
<td align="left"><p>指定工具生成的头文件的名称。 如果未指定路径，则在当前文件夹中生成文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_Memory_Routines"></span><span id="generate_memory_routines"></span><span id="GENERATE_MEMORY_ROUTINES"></span>生成内存例程</p></td>
<td align="left"><p>生成内存分配/可用例行模板。 (<strong>-MemoryRoutines</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_Notification_Callback"></span><span id="generate_notification_callback"></span><span id="GENERATE_NOTIFICATION_CALLBACK"></span>生成通知回调</p></td>
<td align="left"><p>生成自定义通知回调模板。 (<strong>-NotificationCallback</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_resource_file"></span><span id="generate_resource_file"></span><span id="GENERATE_RESOURCE_FILE"></span>生成资源文件</p></td>
<td align="left"><p>指定工具生成的资源文件的名称。 如果未指定路径，则在当前文件夹中生成文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_Summary_Global_File"></span><span id="generate_summary_global_file"></span><span id="GENERATE_SUMMARY_GLOBAL_FILE"></span>生成摘要全局文件</p></td>
<td align="left"><p>生成每个提供程序的二进制计数器文件。 (<strong>-summary</strong> <em>path</em>)</p>
<p>生成摘要全局文件 GenSumResource.BIN。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generated_Counter_Files_Path"></span><span id="generated_counter_files_path"></span><span id="GENERATED_COUNTER_FILES_PATH"></span>生成的计数器文件路径</p></td>
<td align="left"><p>指定生成二进制计数器文件的路径。 (<strong>-sumPath</strong> <em>path</em>)</p>
<p>如果未指定路径，则使用当前目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Header_File_Name_For_Counter"></span><span id="header_file_name_for_counter"></span><span id="HEADER_FILE_NAME_FOR_COUNTER"></span>计数器的头文件名</p></td>
<td align="left"><p>生成包含计数器名称和 ID 的头文件。 (<strong>-ch</strong> <em>filename</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Header_FileName_For_Provider"></span><span id="header_filename_for_provider"></span><span id="HEADER_FILENAME_FOR_PROVIDER"></span>提供程序的头文件名</p></td>
<td align="left"><p>生成提供程序的头文件。 它将替换默认名称。 (<strong>-o</strong> <em>filename</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Resource_File_Name"></span><span id="resource_file_name"></span><span id="RESOURCE_FILE_NAME"></span>资源文件名</p></td>
<td align="left"><p>指定资源文件的名称。 这将替换默认名称。 (<strong>-rc</strong> <em>filename</em>)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idcommentspanspan-idcommentspanspan-idcommentspancomment"></a><span id="Comment"></span><span id="comment"></span><span id="COMMENT"></span>备注


工具所生成文件的默认名称基于你传递到 [**CTRPP**](https://msdn.microsoft.com/Library/Windows/Desktop/aa372128) 工具的清单文件的名称。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [**CTRPP**](https://msdn.microsoft.com/Library/Windows/Desktop/aa372128)
* [性能计数器](https://msdn.microsoft.com/Library/Windows/Desktop/aa373083)
* [内核模式性能监视](https://msdn.microsoft.com/Library/Windows/Hardware/Ff548159)
 

 






