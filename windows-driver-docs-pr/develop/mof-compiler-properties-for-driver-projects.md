---
ms.assetid: 4444E8A5-9624-4CA2-84D8-C83A67A2C871
title: 驱动程序项目的 MOF 编译器属性
description: 托管对象格式 (MOF) 编译器 (mofcomp.exe) 用于解析 MOF 文件并将文件中定义的类和类实例添加到 WMI 存储库中。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5fe74aba3fe87b75c37285202bd714eb7e64784
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364251"
---
# <a name="mof-compiler-properties-for-driver-projects"></a>驱动程序项目的 MOF 编译器属性

托管对象格式 (MOF) 编译器 (mofcomp.exe) 用于解析 MOF 文件并将文件中定义的类和类实例添加到 WMI 存储库中。 使用 Mofcomp 属性页来编译驱动程序的 MOF 文件。 有关 Mofcomp.exe 和 WMI 的详细信息，请参阅 [**mofcomp**](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)、[编译 MOF 文件](https://docs.microsoft.com/windows/desktop/WmiSdk/compiling-mof-files)和[编译驱动程序的 MOF 文件](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)。

## <a name="span-idsetting_managed_object_format__mof__compiler_properties_for_driver_projectsspanspan-idsetting_managed_object_format__mof__compiler_properties_for_driver_projectsspanspan-idsetting_managed_object_format__mof__compiler_properties_for_driver_projectsspansetting-managed-object-format-mof-compiler-properties-for-driver-projects"></a><span id="Setting_Managed_Object_Format__MOF__Compiler_properties_for_driver_projects"></span><span id="setting_managed_object_format__mof__compiler_properties_for_driver_projects"></span><span id="SETTING_MANAGED_OBJECT_FORMAT__MOF__COMPILER_PROPERTIES_FOR_DRIVER_PROJECTS"></span>设置驱动程序项目的托管对象格式 (MOF) 编译器属性


1.  打开驱动程序项目的属性页。 在**解决方案资源管理器**中右键单击驱动程序项目，并选择“属性”  。
2.  在驱动程序项目的属性页中，单击“配置属性”  ，然后单击“Mof 编译器”  。
3.  设置项目属性。

如果你将托管对象格式 (MOF) 文件 (.mof) 添加到解决方案，则此属性页可用。

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
<td align="left"><p><span id="Additional_Options"></span><span id="additional_options"></span><span id="ADDITIONAL_OPTIONS"></span><strong>其他选项</strong></p></td>
<td align="left"><p>指定要传递给 <a href="https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp" data-raw-source="[&lt;strong&gt;mofcomp&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)"><strong>mofcomp</strong></a> 工具的其他选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Amendement"></span><span id="amendement"></span><span id="AMENDEMENT"></span><strong>修订</strong></p></td>
<td align="left"><p>将 MOF 文件拆分成中性语言和特定语言版本。 (<strong>-AMENDMENT:</strong><em>Locale</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Authority"></span><span id="authority"></span><span id="AUTHORITY"></span><strong>颁发机构</strong></p></td>
<td align="left"><p>将 Authority 指定为登录 WMI 时要使用的颁发机构（域名）。 (<strong>-A:</strong><em>Authority</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Auto_Recover"></span><span id="auto_recover"></span><span id="AUTO_RECOVER"></span><strong>自动恢复</strong></p></td>
<td align="left"><p>将命名 MOF 文件添加到在存储库恢复过程中编译的文件列表中。 (<strong>-autorecover</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Create_Binary_Mof_File"></span><span id="create_binary_mof_file"></span><span id="CREATE_BINARY_MOF_FILE"></span><strong>创建二进制 Mof 文件</strong></p></td>
<td align="left"><p>请求编译器使用名称 filename 创建 MOF 文件的二进制版本，而不对 WMI 存储库进行任何修改。 (<strong>-B:</strong><em>Filename</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Language_Neutral_Output"></span><span id="language_neutral_output"></span><span id="LANGUAGE_NEUTRAL_OUTPUT"></span><strong>中性语言输出</strong></p></td>
<td align="left"><p>中性语言输出的名称。 (<strong>-MOF:</strong><em>Path</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Language_Specific_Output"></span><span id="language_specific_output"></span><span id="LANGUAGE_SPECIFIC_OUTPUT"></span><strong>特定语言输出</strong></p></td>
<td align="left"><p>特定语言输出的名称。 (<strong>-MFL:</strong><em>Path</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Mof_Class"></span><span id="mof_class"></span><span id="MOF_CLASS"></span><strong>Mof 类</strong></p></td>
<td align="left"><p>创建或更新 MOF 类。</p>
<p><strong>仅创建 (-class:createonly)</strong> 请求编译器不对现有类做任何更改。 使用此开关时，如果 MOF 文件中指定的类已存在，则编译器操作将会终止。</p>
<p><strong>强制更新 (class:forceupdate)</strong> 当子类存在冲突时，强制更新类。</p>
<p><strong>安全更新 (-class:safeupdate)</strong> 即使存在子类，也允许更新类，只要更改不会导致与子类冲突。</p>
<p><strong>仅更新 (-class:updateonly)</strong> 请求编译器不创建任何新类。</p>
<p></p>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp" data-raw-source="[&lt;strong&gt;mofcomp&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)"><strong>mofcomp</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="NamespacePath"></span><span id="namespacepath"></span><span id="NAMESPACEPATH"></span><strong>NamespacePath</strong></p></td>
<td align="left"><p>请求编译器将 MOF 文件加载到 <em>namespacepath</em> 指定的命名空间。 (<strong>-N:</strong><em>namespacepath</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Resource_Locale"></span><span id="resource_locale"></span><span id="RESOURCE_LOCALE"></span><strong>资源区域设置</strong></p></td>
<td align="left"><p>与 -ER 开关一起使用时，从二进制 MOF 中提取本地化的 MOF 描述。 (<strong>-L:</strong><em>ResourceLocale</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Resource_Name"></span><span id="resource_name"></span><span id="RESOURCE_NAME"></span><strong>资源名称</strong></p></td>
<td align="left"><p>从命名资源中提取二进制 MOF。 (<strong>-ER:</strong><em>ResourceName</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Syntax_Check"></span><span id="syntax_check"></span><span id="SYNTAX_CHECK"></span><strong>语法检查</strong></p></td>
<td align="left"><p>请求编译器仅执行语法检查并打印相应的错误消息。 其他选项均不可与“语法检查”选项搭配使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="WMI_Syntax_Check"></span><span id="wmi_syntax_check"></span><span id="WMI_SYNTAX_CHECK"></span><strong>WMI 语法检查</strong></p></td>
<td align="left"><p>请求编译器执行 WMI 语法检查 <strong>-WMI</strong>。 如果你选择此选项，则必须还选择“创建二进制 Mof 文件”选项 (<strong>-B:</strong><em>Filename</em>)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [编译 MOF 文件](https://docs.microsoft.com/windows/desktop/WmiSdk/compiling-mof-files)
* [编译驱动程序 MOF 文件](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)
* [**mofcomp**](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)
 

 






