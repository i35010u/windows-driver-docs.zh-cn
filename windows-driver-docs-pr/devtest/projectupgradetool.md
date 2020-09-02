---
title: ProjectUpgradeTool
description: ProjectUpgradeTool 采用 Microsoft Visual Studio 2012 项目 (*) 和解决方案文件 (*.sln) 使用 Windows 驱动程序工具包在 windows 8 中创建，并将其升级为适用于 (和) 2013 的 wdk。
ms.assetid: DEB7799C-D505-40E6-B2B0-CF774A99B1BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e08a681fe12436ccfb8ae5ff3f8b4a24b9fe5b7
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382973"
---
# <a name="projectupgradetool"></a>ProjectUpgradeTool


ProjectUpgradeTool Microsoft Visual Studio 采用 2012 (\*) 和解决方案文件 (\* .sln) 使用 Windows 驱动程序工具包（windows 8 的 Windows 驱动程序工具包）进行创建，并将其升级为适用于 (和) 2013 的 wdk。

**重要提示**  ProjectUpgradeTool 不会更改您的源文件。 该工具只转换项目和解决方案文件。 默认情况下，该工具将保存原始文件的备份副本。



**将 WDK 8 项目或解决方案升级到 WDK 8。1**

1.  打开 Visual Studio 命令提示符窗口。
2.  键入命令 **ProjectUpgradeTool** 并指定根 (或父) 目录，其中包含要升级到 Windows 驱动程序工具包的 Windows 驱动程序工具包 (wdk) 8 项目或解决方案文件， (的 wdk) 8.1。 例如，以下命令将升级 C： \\ myDriver 目录和子目录中的所有文件。

    ```
    ProjectUpgradeTool.exe  C:\myDriver
    ```

3.  使用 Visual Studio 2013 打开 WDK 8.1 项目或解决方案文件。 该工具保留文件的原始名称。 以前的版本连同备份文件扩展名一起保存。
    **注意**  如果希望能够为 Windows Vista 生成目标，请使用 Visual Studio 2013 和 WDK 8.1，请参阅 [将 WDK 8 项目迁移到 wdk 8.1 后，如果无法生成 Windows vista 目标，应如何操作](#build-vista-with-wdk-8-1)。



## <a name="span-idprojectupgradetool_syntaxspanspan-idprojectupgradetool_syntaxspanspan-idprojectupgradetool_syntaxspanprojectupgradetool-syntax"></a><span id="ProjectUpgradeTool_Syntax"></span><span id="projectupgradetool_syntax"></span><span id="PROJECTUPGRADETOOL_SYNTAX"></span>ProjectUpgradeTool 语法


项目升级工具位于% WindowsSdkDir% \\ bin \\ x86 \\ 目录中。 例如，C： \\ Program 文件 (x86) \\ Windows 工具包 \\ 8.1 \\ bin \\ x86。

ProjectUpgradeTool.exe 具有以下语法：

```
ProjectUpgradeTool.exe  < rootDir >
                          [-Log:[<LogFile>]:[<Verbosity>]]
                          [-ConsoleLog:<Verbosity>]
                          [-NoBackup]
                          [-NoToolsetUpgrade]
                          [-InPlaceUpgrade]
                          [-ForceUpgrade]
                          [-KeepObsoleteConfigs]   
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-Log：</strong>日志<em> &lt; &gt; 文件</em><strong>： [</strong><em> &lt; 详细级别 &gt; </em><strong>]</strong></p></td>
<td align="left"><p>指定日志文件的名称，并指定日志记录级别 (查看 <em>详细</em> 级别) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ConsoleLog：</strong><em> &lt; 详细 &gt; 级别</em></p></td>
<td align="left"><p>指定控制台日志文件的名称，并指定日志记录级别 (查看 <em>详细</em> 级别) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>程度</em></p></td>
<td align="left"><p>日志文件和控制台日志记录的默认日志记录级别分别为 " <strong>详细</strong> " 和 " <strong>信息</strong> "。 <em>详细级别</em> 是 <strong>SourceLevels</strong>之一。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-NoBackup</strong></p></td>
<td align="left"><p>告诉 ProjectUpgradeTool 不 ( 的原始项目的备份副本) 或 ( .sln) 的解决方案。 如果选择此选项，原始项目和解决方案文件将被覆盖，并且仅适用于 Windows 8.1 和 Visual Studio 2013 的 WDK。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-NoToolsetUpgrade</strong></p></td>
<td align="left"><p>如果在 Windows 8.1 之前指定 Windows 版本的生成配置，请指定 <strong>-NoToolsetUpgrade</strong> 选项，以便在你不希望使用 WDK 8.1 平台工具集。 当你选择此选项时，将仅使用最新的 WDK 生成 <strong>WinPreRel</strong> 配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-InPlaceUpgrade</strong></p></td>
<td align="left"><p>将每个现有的生成配置替换为新的 <strong>WinPreRel</strong> 配置。 这会阻止你为以前版本的 Windows 构建。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-ForceUpgrade</strong></p></td>
<td align="left"><p>强制升级 () 的每个项目文件，即使项目不满足驱动程序项目的要求也是如此。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-KeepObsoleteConfigs</strong></p></td>
<td align="left"><p>保留 WDK (不再支持的操作系统的目标配置，例如，Windows Vista) 。 但是，若要为这些过时目标生成，除了 WDK 8.1 和 Visual Studio 2013，还需要在计算机上安装 Visual Studio 2012 和 WDK 8。 例如，假设你想要升级驱动程序项目，以使用适用于所有受支持的目标版本（ (Windows 7、Windows 8 和 Windows 8.1) ）的 WDK 8.1。 你仍希望使用相同的驱动程序项目来继续为 Windows Vista 构建。 要执行此操作，请使用 <strong>-KeepObsoleteConfigs</strong> 选项升级项目文件，以将 Windows Vista 目标配置保存在项目中。 Windows Vista 配置将继续使用 <strong>windowskernelmodedriver 8.0</strong> 工具集 (在 WDK 8) 中可用，即使您在 Visual Studio 2013 中生成项目也是如此。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>提出


-   [如果 ) 找不到 "MSB8020" (平台工具集 = "WindowsKernelModeDriver 8.0" 时应执行的操作](#what-to-do-if-you-see-error-msb8020)
-   [将 WDK 8 项目迁移到 WDK 8.1 之后，如果无法生成 Windows Vista 目标，该怎么办](#build-vista-with-wdk-8-1)

### <a name="span-idwhat_to_do_if_you_see_error_msb8020__platform_toolset____windowskernelmodedriver80___cannot_be_found_spanspan-idwhat_to_do_if_you_see_error_msb8020__platform_toolset____windowskernelmodedriver80___cannot_be_found_spanspan-idwhat_to_do_if_you_see_error_msb8020__platform_toolset____windowskernelmodedriver80___cannot_be_found_spanwhat-to-do-if-you-see-error-msb8020-platform-toolset--windowskernelmodedriver80-cannot-be-found"></a><span id="What_to_do_if_you_see_Error_MSB8020__Platform_Toolset____WindowsKernelModeDriver8.0___cannot_be_found_"></span><span id="what_to_do_if_you_see_error_msb8020__platform_toolset____windowskernelmodedriver8.0___cannot_be_found_"></span><span id="WHAT_TO_DO_IF_YOU_SEE_ERROR_MSB8020__PLATFORM_TOOLSET____WINDOWSKERNELMODEDRIVER8.0___CANNOT_BE_FOUND_"></span><a name="what-to-do-if-you-see-error-msb8020"></a>如果 ) 找不到 "MSB8020" (平台工具集 = "WindowsKernelModeDriver 8.0" 时应执行的操作

如果尝试打开使用 WDK 8 创建的项目或解决方案，则在尝试使用 WDK 8.1 生成项目时，可能会看到以下错误消息。

```
1>C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V120\Microsoft.Cpp.Platform.targets(54,5): error MSB8020: The builds tools for WindowsKernelModeDriver8.0 (Platform Toolset = 'WindowsKernelModeDriver8.0') cannot be found. To build using the WindowsKernelModeDriver8.0 build tools, please install WindowsKernelModeDriver8.0 build tools. Alternatively, you may update to the current Visual Studio tools by selecting the Project menu or right-click the solution, and then selecting "Update VC++ Projects...".
```

WDK 8 中的平台工具集是 **windowskernelmodedriver 8.0**。 若要修复此错误，请按此处所述运行 ProjectUpgradeTool，并升级 WDK 8 解决方案以使用 WDK 8.1 中提供的工具集

### <a name="span-idbuild_vista_with_wdk_81spanspan-idbuild_vista_with_wdk_81spanspan-idbuild_vista_with_wdk_81spanwhat-to-do-if-you-are-unable-to-build-a-windows-vista-target-after-migrating-a-wdk-8-project-to-wdk-81"></a><span id="build_vista_with_WDK_8.1"></span><span id="build_vista_with_wdk_8.1"></span><span id="BUILD_VISTA_WITH_WDK_8.1"></span><a name="build-vista-with-wdk-8-1"></a>将 WDK 8 项目迁移到 WDK 8.1 之后，如果无法生成 Windows Vista 目标，该怎么办

**问题：** 将 WDK 8 项目迁移到 WDK 8.1 后，无法构建 Windows Vista 目标。

**方案：** 已使用 WDK 8 和 Visual Studio 2012 创建了一个项目。 已使用 ProjectUpgradeTool 工具升级了使用 WDK 8.1 和 Visual Studio 2013 的项目/解决方案。 为此，请使用以下命令保留 Windows Vista 配置： **ProjectUpgradeTool.exe** *PathToProjectFolder* **-KeepObsoleteConfigs。**

在 WDK 8.1 中打开该项目。 生成 Win32 Windows Vista 目标时，可能会看到以下错误消息：

```
error MSB6004: The specified task executable location "C:\Program Files (x86)\Windows Kits\8.0\bin\x86\x86\CL.exe" is invalid.   C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V110\Microsoft.CppCommon.targets  347 5   KMDF Driver1
```

构建 x64 Windows Vista 目标时，可能会看到以下错误消息：

```
error TRK0002: Failed to execute command: ""C:\Program Files (x86)\Windows Kits\8.0\bin\x64\stampinf.exe" -d * -a amd64 -v * -k 1.11 -u 1.11.0 -f x64\VistaRelease\KMDFDriver1.inf". The operation identifier is not valid.  C:\Users\Administrator\Desktop\KMDF Driver1 - Copy\KMDF Driver1\TRACKER KMDF Driver1
```

```
error : Verification Error: Driver package has no driver version.    C:\Program Files (x86)\Windows Kits\8.0\build\WindowsDriver8.0.common.targets   1338    5   KMDF Driver1 Package
```

**解决方法：** 需要进行两次更改。

1.  **更正 WindowsDriver 属性和 WindowsDriver 8.0. 属性文件。**

    需要在这两个属性文件的条件表达式中进行更正 \* 。 文件位于 C： \\ Program files (x86) \\ Windows 工具包 \\ 8.0 \\ 生成目录中。

    在每个 \* 属性文件中，找到表达式 where `('$(VisualStudioVersion)' != '11.0')` 。 例如，第一个实例将如下所示：

    ```XML
            <When  Condition="'$(VisualStudioVersion)' != '11.0'">
          <PropertyGroup>
            <CLToolPath Condition="'$(CLToolPath)' == ''">$(WDKContentRoot)bin\x86\x64</CLToolPath>
            <CLToolArchitecture>Native32Bit</CLToolArchitecture>
            <LinkToolPath Condition="'$(LinkToolPath)' == ''">$(WDKContentRoot)bin\x86\x64</LinkToolPath>
            <LinkToolArchitecture>Native32Bit</LinkToolArchitecture>
            <MIDLToolPath Condition="'$(MIDLToolPath)' == ''">$(WDKContentRoot)bin\x86</MIDLToolPath>
            <MIDLToolArchitecture>Native32Bit</MIDLToolArchitecture>
            <LibToolPath Condition="'$(LibToolPath)' == ''">$(WDKContentRoot)bin\x86</LibToolPath>
            <LibToolArchitecture>Native32Bit</LibToolArchitecture>
            <ExecutablePath>$(WDKContentRoot)bin\x86\x64;$(WDKContentRoot)bin\x86;$(WDKContentRoot)tools\pfd\bin\bin\AMD64;$(WDKContentRoot)tools\tracing\x64;$(ExecutablePath)</ExecutablePath>      
        </PropertyGroup>
        </When>
    ```

    将 not 等于 (！ =) 改为小于 ( " &lt; " ) 。

    ```XML
        <When  Condition="'$(VisualStudioVersion)' &lt;'11.0'">
    ```

    找到表达式的下一个实例，其中 `('$(VisualStudioVersion)' != '11.0')`

    ```XML
        <When Condition="('$(PlatformToolset)' == 'WindowsApplicationForDrivers8.0') and ('$(VisualStudioVersion)' != '11.0')">
    ```

    然后将 not 等于 (！ =) 改为小于 ( " &lt; " ) 。

    ```XML
        <When Condition="('$(PlatformToolset)' == 'WindowsApplicationForDrivers8.0') and ('$(VisualStudioVersion)' &lt;'11.0')">
    ```

    进行更改后，请保存这两个 \* 属性文件。

2.  **更正驱动程序的项目文件。**

    为驱动程序打开项目文件 (" \* .vcxproj") 。

    在项目文件中找到 Vista 目标配置 ("发布并调试") 。 例如：

    ```XML
       <PropertyGroup Label="Configuration" Condition="'$(Configuration)|$(Platform)'=='Vista Debug|Win32'">
        <TargetVersion>Vista</TargetVersion>
        <UseDebugLibraries>True</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    将 **PackageDir** 属性添加到 Windows Vista 配置设置。 在大多数情况下，应使用默认值： `<PackageDir>$(OutDir)\$(Intdir)</PackageDir>` 。

    ```XML
       <PropertyGroup Label="Configuration" Condition="'$(Configuration)|$(Platform)'=='Vista Debug|Win32'">
        <TargetVersion>Vista</TargetVersion>
        <PackageDir>$(OutDir)\$(Intdir)</PackageDir>
        <UseDebugLibraries>True</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    对其他配置进行相同的更改。

    ```XML
        <PropertyGroup Label="Configuration" Condition="'$(Configuration)|$(Platform)'=='Vista Release|Win32'">
        <TargetVersion>Vista</TargetVersion>
        <PackageDir>$(OutDir)\$(Intdir)</PackageDir>
        <UseDebugLibraries>False</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    进行这些更改并保存文件后，可以在 Visual Studio 2013 中打开并生成项目。 项目应继续使用 Visual Studio 2012。 请注意，即使在这些更改之后，计算机上仍需要安装 WDK 8 和 Visual Studio 2012。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[生成驱动程序](../develop/building-a-driver.md)

[WDK 和 Visual Studio 生成环境](wdk-and-visual-studio-build-environment.md)