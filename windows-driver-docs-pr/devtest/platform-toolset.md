---
title: 平台工具集
description: Windows Driver Kit (WDK) 利用 MSBuild 平台工具集功能提供的工具和特定于驱动程序开发的库。
ms.assetid: 9F585CA3-B863-408A-B785-2456460D6626
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf72527e93fedd2f1865ea4dc246b34952e99e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541620"
---
# <a name="platform-toolset"></a>平台工具集


Windows Driver Kit (WDK) 利用 MSBuild 平台工具集功能提供的工具和特定于驱动程序开发的库。 MSBuild 平台工具集功能进行扩展。 由 MSBuild 属性名为控制你想要使用的平台工具集的特定版本**PlatformToolset**。 项目可以通过设置工具和库之间切换**PlatformToolset**项目文件中的属性。

Windows Driver Kit (WDK) 8.1 为驱动程序开发提供了以下平台工具集。

| **PlatformToolset** (WDK 8.1)       | 将                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WindowsKernelModeDriver8.1**      | 内核模式驱动程序和组件。                                                                                                                                                                                                                                                                                                                                                     |
| **WindowsUserModeDriver8.1**        | 用户模式驱动程序和组件。                                                                                                                                                                                                                                                                                                                                                       |
| **WindowsApplicationForDrivers8.1** | 任何类型的应用程序。 此平台工具集提供与针对 Windows 7 (WDK 7.1) 中，使用 Windows Driver Kit (WDK) 中的生成选项的兼容性，并使用常见的开发与驱动程序进行交互的用户模式应用程序的默认设置。 如果你正在迁移或使用 WDK 7 生成的项目转换，可能会使用此设置。 |
| **Visual Studio 2013 (v120)**       | 使用任何类型的 Windows 应用程序 （默认值）。                                                                                                                                                                                                                                                                                                                                          |

 

Windows Driver Kit (WDK) 8 为驱动程序开发提供以下平台工具集。 仅适用于参考提供此信息。

| **PlatformToolset** (WDK 8)         | 将                                                                                                                                                                                                                                           |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WindowsKernelModeDriver8.0**      | 内核模式驱动程序和组件。                                                                                                                                                                                                       |
| **WindowsUserModeDriver8.0**        | 用户模式驱动程序和组件。                                                                                                                                                                                                         |
| **WindowsApplicationForDrivers8.0** | 任何类型的应用程序。 此平台工具集提供了与在 WDK 适用于 Windows 7 (WDK 7.1) 中使用的生成选项的兼容性。 如果你正在迁移或使用 WDK 7 生成的项目转换，可能会使用此设置。 |
| **Visual Studio 2012 (v110)**       | 使用任何类型的 Windows 应用程序 （默认值）。                                                                                                                                                                                            |

 

**请注意**  如果从 Visual Studio 中可用的 Windows 驱动程序模板之一创建驱动程序**PlatformToolset**属性设置为你。 您还可以选择**PlatformToolset**通过使用 Visual Studio 中的驱动程序项目属性页。
**在 Visual Studio 中设置的平台工具集**

1.  打开你的驱动程序项目的属性页。 在**解决方案资源管理器**中右键单击驱动程序项目，并选择**属性**。
2.  在驱动程序项目的属性页中，单击**配置属性**，然后单击**常规**。
3.  选择**平台工具集**下拉列表中的项目的属性。

 

## <a name="span-idexample-settingtheplatformtoolsetpropertyinavisualstudioprojectfilevcxprojspanspan-idexample-settingtheplatformtoolsetpropertyinavisualstudioprojectfilevcxprojspanspan-idexample-settingtheplatformtoolsetpropertyinavisualstudioprojectfilevcxprojspanexample---setting-the-platformtoolset-property-in-a-visual-studio-project-file-vcxproj"></a><span id="Example_-_Setting_the_PlatformToolset_property_in_a_Visual_Studio_project_file__.vcxproj_"></span><span id="example_-_setting_the_platformtoolset_property_in_a_visual_studio_project_file__.vcxproj_"></span><span id="EXAMPLE_-_SETTING_THE_PLATFORMTOOLSET_PROPERTY_IN_A_VISUAL_STUDIO_PROJECT_FILE__.VCXPROJ_"></span>示例-设置**PlatformToolset** Visual Studio 项目文件 (.vcxproj) 中的属性


下面的示例演示如何**PlatformToolset**在项目文件中设置属性。

```XML
<PropertyGroup Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Debug|Win32&#39;"
      Label="Configuration">
  <ConfigurationType>Driver</ConfigurationType>
  <DriverType>KMDF</DriverType>
  <PlatformToolset>WindowsKernelModeDriver8.1</PlatformToolset>
</PropertyGroup>
```

**配置类型**属性控制在目标扩展和二进制文件所生成的输出类型。 此属性的可能值的一些**应用程序**， **DynamicLibrary**， **StaticLibrary**，以及**实用工具**。

WDK 引入了名为此属性的新值**驱动程序**来生成内核模式驱动程序。 如果此属性设置为**驱动程序**，MSBuild 将生成具有.sys 作为其扩展的驱动程序文件。 在示例中， **PlatformToolset**属性设置为**WindowsKernelModeDriver8.1**来生成内核模式驱动程序。 **WindowsKernelModeDriver8.1**是唯一的 WDK 平台工具集，需要**DriverConfigurationType**。 在此示例中， **DriverType**设置为 KMDF。

## <a name="span-idabouttheplatformtoolsetpropertyfordriversspanspan-idabouttheplatformtoolsetpropertyfordriversspanspan-idabouttheplatformtoolsetpropertyfordriversspanabout-the-platformtoolset-property-for-drivers"></a><span id="About_the_PlatformToolset_property_for_drivers"></span><span id="about_the_platformtoolset_property_for_drivers"></span><span id="ABOUT_THE_PLATFORMTOOLSET_PROPERTY_FOR_DRIVERS"></span>有关**PlatformToolset**驱动程序的属性


**PlatformToolset**是一组的属性表、 目标、 工具和任务，它们共同协作以扩展和修改一个平台，以便生成驱动程序或该特定平台的内核模式组件。 驱动程序和相关的组件和应用程序， **PlatformToolset**属性应设置为**WindowsKernelModeDriver8.1**， **WindowsUserModeDriver8.1**，或**WindowsApplicationForDrivers8.1**项目文件中。 这些平台工具集旨在扩展现有的 Visual Studio C\\c + + 工具链编译器和链接器使用其他 WDK 特定应在 WDK 标头和库生成工具和目标。 **WindowsApplicationForDrivers8.1**工具集提供与生成的兼容性选项设置在 WDK 适用于 Windows 7 (WDK 7.1) 中提供且还默认设置通用开发的用户模式与驱动程序进行交互的应用程序。

**平台工具集**具有默认平台级别设置和目标，以便生成任何驱动程序项目。 使用如编译器或链接器生成工具，例如有关 WDK、 INCLUDE 或库路径的系统信息和功能设置，例如各个属性的默认开关，若要使用 Unicode 或 ANSI 字符串可以生成一个驱动程序时，设置。 如果要开发适用于桌面的 Windows 应用程序，请不要使用**WindowsKernelModeDriver8.1**， **WindowsUserModeDriver8.1**，或**WindowsApplicationForDrivers8.1**平台工具集。 请改用**Visual Studio 2013 (v120)** 平台工具集。

默认情况下**PlatformToolset**属性是**Visual Studio 2013 (v120)** 用于新创建 Win32 用户模式 c + + 项目和已转换为 Visual Studio 2013 的项目。 在这两种情况下， **PlatformToolset**属性不会写入项目文件。

当你选择其中一个驱动程序的平台工具集时，设置以下属性。

-   ExecutablePath 和 NativeExecutablePath （路径）
-   IncludePath (INCLUDE)
-   ReferencePath (的 LIBPATH)
-   LibraryPath (LIB)
-   SourcePath
-   ExcludedPath

**请注意**  时**UseEnv**未设置为**TRUE**，将从相应的属性值中的平台工具集设置的路径、 LIB、 INCLUDE、 LIBPATH。 当**UseEnv**设置为**TRUE**，如下所示旧生成系统，将改为使用 PATH、 INCLUDE、 LIB 和 LIBPATH 环境变量中的值。

 

## <a name="span-idwherethewdkinstallsfilesthatenablethedriver-specificplatformtoolsetsspanspan-idwherethewdkinstallsfilesthatenablethedriver-specificplatformtoolsetsspanspan-idwherethewdkinstallsfilesthatenablethedriver-specificplatformtoolsetsspanwhere-the-wdk-installs-files-that-enable-the-driver-specific-platform-toolsets"></a><span id="Where_the_WDK_installs_files_that_enable_the_driver-specific_platform_toolsets"></span><span id="where_the_wdk_installs_files_that_enable_the_driver-specific_platform_toolsets"></span><span id="WHERE_THE_WDK_INSTALLS_FILES_THAT_ENABLE_THE_DRIVER-SPECIFIC_PLATFORM_TOOLSETS"></span>WDK 安装启用特定于驱动程序的平台工具集的文件的位置


下表总结了 WDK 安装文件，以使驱动程序开发的平台工具集的位置的位置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">路径变量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>$ （vctargetspath)</p></td>
<td align="left"><p>默认情况下，$ （vctargetspath） 定义在注册表中作为 $(MSBuildExtensionsPath)&lt;全身&gt;&lt;文件夹&gt;</em>&amp;l t;MSBUILDSYNTAXVERSION&gt;)</p>
<p>在新的生成过程使用的相同平台的具有新语法，并且需要更高版本的 MSBuild 的情况下，是包含的版本号。</p>
<p><em>&lt;文件夹&gt;</em>是<strong>Microsoft.Cpp</strong>文件夹-$(MSBuildExtensionsPath)\Microsoft.Cpp\4.0\v120。</p>
<p>这称为<em>语法版本</em>而非<em>工具版本</em>。 它是第一个程序集版本<strong>Microsoft.Build.Engine</strong>支持的所有必要的语法。 <strong>Microsoft.Cpp</strong>指示 Visual Studio 将查找平台的唯一文件夹。</p></td>
</tr>
<tr class="even">
<td align="left"><p>$(VCTargetsPath)\Platforms$(Platform)\ImportAfter<em>.props</p></td>
<td align="left"><p>通常情况下不包含文件的可选文件夹。 通过将 MSBuild 格式文件保存在此文件夹中，可以自定义平台。 它们将导入在底部的平台设置文件，由当前正在的文件夹。 从该位置，将导入文件的顺序是未定义。 MSBuild 创建的文件是 $(VCTargetsPath) \Platforms$ （平台） \ImportAfter\Microsoft.Cpp。<em>&lt;平台&gt;</em>。WindowsKernelModeDriver8.1.props 和 Microsoft.Cpp。<em>&lt;平台&gt;</em>。WindowsUserModeDriver8.1.props 导入多个特定于 WDK 的属性文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>$(VCTargetsPath)\Platforms$(Platform)\PlatformToolsets$(PlatformToolset)&lt;/p&gt;</td>
<td align="left"><p>针对 WDK:</p>
<p><strong>$(PlatformToolset)</strong>必须设置为<strong>WindowsKernelModeDriver8.1</strong>对于生成内核模式驱动程序，将设置为<strong>WindowsUserModeDriver8.1</strong>用于生成用户模式驱动程序，并将设置为<strong>WindowsApplicationForDrivers8.1</strong>与在 Windows 7 WDK (WDK 7) 中使用的生成选项的兼容性。</p>
<p><strong>PlatformToolset 目录</strong></p>
<p>例如，C:\Program Files\MSBuild\Microsoft.Cpp\v4.0\v120\Platforms\Win32\PlatformToolsets\WindowsKernelModeDriver8.1。</p>
<p>PlatformToolsets 目录，可在其自己的子文件夹中添加其他类型的更高版本 – 文件。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>Microsoft.Cpp.$ （平台）。 $(PlatformToolset).props</p></td>
<td align="left"><p><strong>平台工具集属性文件</strong></p>
<p>导入属性文件以生成驱动程序。 此外会导入 v120 属性文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft.Cpp.$ （平台）。 $(PlatformToolset).targets</p></td>
<td align="left"><p><strong>平台工具集目标文件</strong></p>
<p>导入目标文件，以生成驱动程序。 这些文件包含&lt;UsingTask&gt;标记，以拉入 WDK 任务。 此功能还会导入 v120 目标。</p></td>
</tr>
<tr class="even">
<td align="left"><p>$(WDKContentRoot) \build</em>.props</p></td>
<td align="left"><p>所有驱动程序特定属性文件。 这些文件包含默认设置，以生成驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>$(WDKContentRoot)\build*.targets</p></td>
<td align="left"><p>所有驱动程序特定的目标文件。 此文件来确定要生成一个驱动程序的目标。</p></td>
</tr>
</tbody>
</table>

 

 

 





