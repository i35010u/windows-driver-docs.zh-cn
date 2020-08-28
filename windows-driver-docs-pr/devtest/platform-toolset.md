---
title: 平台工具集
description: Windows 驱动程序工具包 (WDK) 利用 MSBuild 平台工具集功能提供特定于驱动程序开发的工具和库。
ms.assetid: 9F585CA3-B863-408A-B785-2456460D6626
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20a0cf485c13ae0ce375fc216c343b8ec5b3ca0b
ms.sourcegitcommit: 9e5a99dc75dfee3caa9a242adc0ed22ae4df9f29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89043159"
---
# <a name="platform-toolset"></a>平台工具集


Windows 驱动程序工具包 (WDK) 利用 MSBuild 平台工具集功能提供特定于驱动程序开发的工具和库。 MSBuild 平台工具集功能是可扩展的。 要使用的平台工具集的特定版本由名为 **PlatformToolset**的 MSBuild 属性控制。 项目可通过设置项目文件中的 **PlatformToolset** 属性在工具和库之间切换。

Windows 驱动程序工具包 (WDK) 8.1 为驱动程序开发提供了以下平台工具集。

| **PlatformToolset** (WDK 8.1)        | 用途                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WindowsKernelModeDriver 8。1**      | 用于内核模式驱动程序和组件。                                                                                                                                                                                                                                                                                                                                                     |
| **WindowsUserModeDriver 8。1**        | 适用于用户模式驱动程序和组件。                                                                                                                                                                                                                                                                                                                                                       |
| **WindowsApplicationForDrivers 8。1** | 适用于任何类型的应用程序。 此平台工具集为 Windows 7 (WDK 7.1) 中的 Windows 驱动程序工具包 (WDK) 中使用的生成选项提供兼容性，并且还使用用于开发与驱动程序交互的用户模式应用程序的默认设置。 如果要迁移或转换使用 WDK 7 生成的项目，可以使用此设置。 |
| **Visual Studio 2013 (v120) **       | 将用于任何类型的 Windows 应用程序 (默认) 。                                                                                                                                                                                                                                                                                                                                          |

 

Windows 驱动程序工具包 (WDK) 8 为驱动程序开发提供了以下平台工具集。 此信息仅供参考。

| **PlatformToolset** (WDK 8)          | 用途                                                                                                                                                                                                                                           |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WindowsKernelModeDriver 8。0**      | 用于内核模式驱动程序和组件。                                                                                                                                                                                                       |
| **WindowsUserModeDriver 8。0**        | 适用于用户模式驱动程序和组件。                                                                                                                                                                                                         |
| **WindowsApplicationForDrivers 8。0** | 适用于任何类型的应用程序。 此平台工具集与用于 Windows 7 (WDK 7.1) 的 WDK 中使用的生成选项兼容。 如果要迁移或转换使用 WDK 7 生成的项目，可以使用此设置。 |
| **Visual Studio 2012 (v110) **       | 将用于任何类型的 Windows 应用程序 (默认) 。                                                                                                                                                                                            |

 

**注意**   如果从 Visual Studio 中的一个可用 Windows 驱动程序模板创建驱动程序，则会为你设置**PlatformToolset**属性。 还可以通过使用 Visual Studio 中的 "驱动程序项目" 属性页选择 **PlatformToolset** 。
**在 Visual Studio 中设置平台工具集**

1.  打开驱动程序项目的属性页。 选择并按住 (或右键单击) **解决方案资源管理器** 中的驱动程序项目，然后选择 " **属性**"。
2.  在驱动程序项目的属性页中，选择 " **配置属性** "，然后选择 " **常规**"。
3.  从下拉列表中选择项目的 " **平台工具集** " 属性。

 

## <a name="span-idexample_-_setting_the_platformtoolset_property_in_a_visual_studio_project_file__vcxproj_spanspan-idexample_-_setting_the_platformtoolset_property_in_a_visual_studio_project_file__vcxproj_spanspan-idexample_-_setting_the_platformtoolset_property_in_a_visual_studio_project_file__vcxproj_spanexample---setting-the-platformtoolset-property-in-a-visual-studio-project-file-vcxproj"></a><span id="Example_-_Setting_the_PlatformToolset_property_in_a_Visual_Studio_project_file__.vcxproj_"></span><span id="example_-_setting_the_platformtoolset_property_in_a_visual_studio_project_file__.vcxproj_"></span><span id="EXAMPLE_-_SETTING_THE_PLATFORMTOOLSET_PROPERTY_IN_A_VISUAL_STUDIO_PROJECT_FILE__.VCXPROJ_"></span>示例-设置 Visual Studio 项目文件中的 **PlatformToolset** 属性 (. .vcxproj) 


下面的示例演示如何在项目文件中设置 **PlatformToolset** 属性。

```XML
<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'"
      Label="Configuration">
  <ConfigurationType>Driver</ConfigurationType>
  <DriverType>KMDF</DriverType>
  <PlatformToolset>WindowsKernelModeDriver8.1</PlatformToolset>
</PropertyGroup>
```

**配置类型**属性控制正在生成的二进制文件的目标扩展名和输出类型。 此属性的某些可能值为 **Application**、 **例如 dynamiclibrary**、 **StaticLibrary**和 **Utility**。

WDK 为此属性引入了一个新值，称为 " **驱动程序** " 来构建内核模式驱动程序。 如果将此属性设置为 " **驱动程序**"，MSBuild 将生成一个包含 .sys 作为其扩展名的驱动程序文件。 在此示例中， **PlatformToolset** 属性设置为 **windowskernelmodedriver 8.1** 来构建内核模式驱动程序。 **Windowskernelmodedriver 8.1** 是唯一需要 **DriverConfigurationType**的 WDK 平台工具集。 在此示例中， **DriverType** 设置为 KMDF。

## <a name="span-idabout_the_platformtoolset_property_for_driversspanspan-idabout_the_platformtoolset_property_for_driversspanspan-idabout_the_platformtoolset_property_for_driversspanabout-the-platformtoolset-property-for-drivers"></a><span id="About_the_PlatformToolset_property_for_drivers"></span><span id="about_the_platformtoolset_property_for_drivers"></span><span id="ABOUT_THE_PLATFORMTOOLSET_PROPERTY_FOR_DRIVERS"></span>关于驱动程序的 **PlatformToolset** 属性


**PlatformToolset**是一组属性表、目标、工具和任务，它们协同工作以扩展和修改平台，以便为该特定平台构建驱动程序或内核模式组件。 对于驱动程序和相关的组件和应用程序， **PlatformToolset** 属性应在项目文件中设置为 **windowskernelmodedriver 8.1**、 **windowsusermodedriver 8.1**或 **windowsapplicationfordrivers 8.1** 。 这些平台工具集旨在扩展现有的 Visual Studio C \\ + + 工具链编译器和链接器与其他特定于 wdk 的生成工具，并面向 wdk 标头和库。 **Windowsapplicationfordrivers 8.1**工具集提供与适用于 Windows 7 (wdk 7.1) 的 wdk 中可用的生成选项设置的兼容性，以及用于开发与驱动程序交互的用户模式应用程序的默认设置。

**平台工具集**具有用于生成任何驱动程序项目的默认平台级别设置和目标。 将默认开关用于生成工具（例如编译器或链接器）、系统信息（如 WDK 的包含或库路径）和功能设置（如使用 Unicode 或 ANSI 字符串生成驱动程序项目时要设置的各种属性）。 如果要为桌面开发 Windows 应用程序，请不要使用 **windowskernelmodedriver 8.1**、 **Windowsusermodedriver 8.1**或 **windowsapplicationfordrivers 8.1** 平台工具集。 请改用 **Visual Studio 2013 (v120) ** 平台工具集。

默认情况下，对于新创建的 Win32 用户模式 c + + 项目和已转换为 Visual Studio 2013 的项目， **PlatformToolset** 属性 **Visual Studio 2013 (v120) ** 。 在这两种情况下， **PlatformToolset** 属性不会写入项目文件。

为驱动程序选择一个平台工具集时，将设置以下属性。

-   ExecutablePath 和 NativeExecutablePath (路径) 
-   IncludePath (包括) 
-   ReferencePath (LIBPATH) 
-   LibraryPath (LIB) 
-   SourcePath
-   ExcludedPath

**注意**   如果**UseEnv**未设置为**TRUE**，则将从平台工具集中的相应属性值设置 PATH、LIB、INCLUDE、LIBPATH。 当 **UseEnv** 设置为 **TRUE**时，与在旧生成系统中一样，将改为使用 PATH、INCLUDE、LIB 和 LIBPATH 环境变量中的值。

 

## <a name="span-idwhere_the_wdk_installs_files_that_enable_the_driver-specific_platform_toolsetsspanspan-idwhere_the_wdk_installs_files_that_enable_the_driver-specific_platform_toolsetsspanspan-idwhere_the_wdk_installs_files_that_enable_the_driver-specific_platform_toolsetsspanwhere-the-wdk-installs-files-that-enable-the-driver-specific-platform-toolsets"></a><span id="Where_the_WDK_installs_files_that_enable_the_driver-specific_platform_toolsets"></span><span id="where_the_wdk_installs_files_that_enable_the_driver-specific_platform_toolsets"></span><span id="WHERE_THE_WDK_INSTALLS_FILES_THAT_ENABLE_THE_DRIVER-SPECIFIC_PLATFORM_TOOLSETS"></span>WDK 安装文件的位置，这些文件启用了特定于驱动程序的平台工具集


下表总结了 WDK 安装文件以启用用于驱动程序开发的平台工具集的位置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">路径变量</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>$ (VCTargetsPath) </p></td>
<td align="left"><p>默认情况下，注册表中将 $ (VCTargetsPath) 定义为 $ (MSBuildExtensionsPath) &lt; em &gt; &lt; 文件夹 &gt; </em> &lt; MSBUILDSYNTAXVERSION &gt;) </p>
<p>如果将新的生成过程用于同一平台（具有新语法并且需要更高版本的 MSBuild），则会包含版本号。</p>
<p><em> &lt; 文件夹 &gt; </em>是<strong>Microsoft .Cpp</strong>文件夹-$ (MSBuildExtensionsPath) \microsoft.cpp\4.0\v120。</p>
<p>这称为 <em>语法版本</em> ，而不是 <em>工具版本</em>。 它是支持所有必要语法的第一个 <strong>Microsoft. Engine</strong> 的程序集版本。 在 Visual Studio 查找平台时，只有一个<strong>文件夹。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>$ (VCTargetsPath) \Platforms $ (平台) \ImportAfter <em> 属性</p></td>
<td align="left"><p>通常不包含文件的可选文件夹。 可以通过将 MSBuild 格式文件保存在此文件夹中来自定义平台。 它们将导入到平台设置文件的底部，如当前所在文件夹所示。 从该位置导入文件的顺序是不确定的。 MSBuild 创建的文件是 $ (VCTargetsPath) \Platforms $ (平台) \ImportAfter\Microsoft.Cpp。<em> &lt; 平台 &gt; </em>。WindowsKernelModeDriver 8.1. 属性和。<em> &lt; 平台 &gt; </em>。WindowsUserModeDriver 8.1. 属性，用于导入几个特定于 WDK 的属性文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>$ (VCTargetsPath) \Platforms $ (平台) \PlatformToolsets $ (PlatformToolset) &lt; /p&gt;</td>
<td align="left"><p>对于 WDK：</p>
<p><strong>$ (PlatformToolset) </strong>必须设置为<strong>windowskernelmodedriver 8.1</strong>才能构建内核模式驱动程序，将其设置为<strong>windowsusermodedriver 8.1</strong>用于构建用户模式驱动程序，并将设置为<strong>WINDOWSAPPLICATIONFORDRIVERS 8.1</strong> ，以与 Windows 7 wdk (wdk 7) 中使用的生成选项兼容。</p>
<p><strong>PlatformToolset 目录</strong></p>
<p>例如，C:\Program Files\MSBuild\Microsoft.Cpp\v4.0\v120\Platforms\Win32\PlatformToolsets\WindowsKernelModeDriver8.1。</p>
<p>PlatformToolsets 目录允许稍后添加其他类型的文件–在其自己的子文件夹中。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>属性 (平台) $ (PlatformToolset) 。</p></td>
<td align="left"><p><strong>平台工具集属性文件</strong></p>
<p>导入用于构建驱动程序的属性文件。 还会导入 v120 属性文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p> (平台) $ (PlatformToolset) 目标</p></td>
<td align="left"><p><strong>平台工具集目标文件</strong></p>
<p>导入用于构建驱动程序的目标文件。 这些文件包含 &lt; &gt; 用于请求 WDK 任务的 UsingTask 标记。 此功能还会导入 v120 目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>$ (WDKContentRoot) \build </em> . 属性</p></td>
<td align="left"><p>所有驱动程序特定的属性文件。 这些文件包含用于构建驱动程序的默认设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>$ (WDKContentRoot) \build * .targets</p></td>
<td align="left"><p>所有驱动程序特定目标文件。 此文件标识用于构建驱动程序的目标。</p></td>
</tr>
</tbody>
</table>

 

 

 





