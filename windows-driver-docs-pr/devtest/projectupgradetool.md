---
title: ProjectUpgradeTool
description: ProjectUpgradeTool 采用 Microsoft Visual Studio 2012 项目 (*.vcxproj) 和解决方案文件 (*.sln)，适用于 Windows 8 创建使用 Windows Driver Kit (WDK) 和升级其可用于 Windows 8.1 的 WDK 和Microsoft Visual Studio 2013。
ms.assetid: DEB7799C-D505-40E6-B2B0-CF774A99B1BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 721587fdeadc05d616f68b66aadb381ab87ea207
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526227"
---
# <a name="projectupgradetool"></a>ProjectUpgradeTool


ProjectUpgradeTool 采用 Microsoft Visual Studio 2012 项目 (\*.vcxproj) 和解决方案文件 (\*.sln)，适用于 Windows 8 创建使用 Windows Driver Kit (WDK) 和升级其可用于 Windows 8.1 的 WDK 和Microsoft Visual Studio 2013。

**重要**ProjectUpgradeTool 不会更改的源文件。 该工具仅将转换的项目和解决方案文件。 默认情况下，该工具将保存原始文件的备份副本。



**若要升级到 WDK 8.1 WDK 8 项目或解决方案**

1.  打开 Visual Studio 命令提示符窗口。
2.  键入命令**ProjectUpgradeTool**并指定包含想要升级到 Windows Driver Kit (WDK) 8.1 的 Windows 8.1 的 Windows Driver Kit (WDK) 8 项目或解决方案文件的根 （或父） 目录。 例如，以下命令将升级 c： 驱动器中的所有文件\\myDriver 目录和子目录。

    ```
    ProjectUpgradeTool.exe  C:\myDriver
    ```

3.  打开使用 Visual Studio 2013 的 WDK 8.1 项目或解决方案文件。 该工具将保持原始文件的名称。 使用.backup 文件扩展名保存以前的版本。
    **请注意**如果你想要能够生成适用于 Windows Vista 的目标，使用 Visual Studio 2013 和 WDK 8.1，请参阅[要执行的操作如果无法将 WDK 8 项目迁移到 WDK 8.1 后生成的 Windows Vista 目标](#build-vista-with-wdk-8-1)。



## <a name="span-idprojectupgradetoolsyntaxspanspan-idprojectupgradetoolsyntaxspanspan-idprojectupgradetoolsyntaxspanprojectupgradetool-syntax"></a><span id="ProjectUpgradeTool_Syntax"></span><span id="projectupgradetool_syntax"></span><span id="PROJECTUPGRADETOOL_SYNTAX"></span>ProjectUpgradeTool 语法


项目升级工具位于 %windowssdkdir%\\bin\\x86\\目录。 例如，c:\\Program Files (x86)\\Windows 工具包\\8.1\\bin\\x86。

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
<td align="left"><p><strong>-Log:</strong><em>&lt;LogFile&gt;</em><strong>: [</strong><em>&lt;详细级别&gt;</em><strong>]</strong></p></td>
<td align="left"><p>指定日志文件的名称和指定的日志记录级别 (请参阅<em>详细级别</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ConsoleLog:</strong><em>&lt;详细级别&gt;</em></p></td>
<td align="left"><p>指定控制台日志文件的名称和指定的日志记录级别 (请参阅<em>详细级别</em>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>详细级别</em></p></td>
<td align="left"><p>默认日志记录级别的日志文件和控制台日志记录<strong>Verbose</strong>并<strong>信息</strong>分别。 <em>详细程度</em>是之一<strong>System.Diagnostics.SourceLevels</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-NoBackup</strong></p></td>
<td align="left"><p>告知 ProjectUpgradeTool 不以制作备份副本的原始项目 (.vcxproj) 或解决方案 (.sln)。 如果选择此选项时，原始项目和解决方案文件覆盖，并将仅适用于 Windows 8.1 的 WDK 和 Visual Studio 2013。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-NoToolsetUpgrade</strong></p></td>
<td align="left"><p>指定<strong>-NoToolsetUpgrade</strong>选项如果您不想要指定 Windows 8.1 之前的 Windows 版本的生成配置时使用 WDK 8.1 平台工具集。 当选择此选项时，只有<strong>WinPreRel</strong>将使用最新的 WDK 构建配置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-InPlaceUpgrade</strong></p></td>
<td align="left"><p>使用新替换每个现有的生成配置<strong>WinPreRel</strong>配置。 这样可防止您从以前版本的 Windows 构建。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-ForceUpgrade</strong></p></td>
<td align="left"><p>强制升级，每个项目文件 (.vcxproj)，即使该项目不符合要求的驱动程序项目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-KeepObsoleteConfigs</strong></p></td>
<td align="left"><p>将保留通过 WDK (例如，Windows Vista) 不再受支持的操作系统的目标配置。 但是，若要生成为这些已过时的目标，需要具有 Visual Studio 2012 和除了 WDK 8.1 和 Visual Studio 2013 的计算机上安装 WDK 8。 例如，假设你想要升级该驱动程序项目以使用 WDK 8.1 的所有支持的目标版本 （Windows 7、 Windows 8 和 Windows 8.1）。 并且你仍想要使用相同的驱动程序项目来为 Windows Vista 中继续生成。 若要执行此操作，则升级项目文件使用<strong>-KeepObsoleteConfigs</strong>选项可以使 Windows Vista 目标配置项目中。 Windows Vista 配置将继续使用<strong>WindowsKernelModeDriver8.0</strong>的工具集 （WDK 8 中提供），即使生成 Visual Studio 2013 中的项目。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>注释


-   [要执行的操作如果看到错误 MSB8020 (平台工具集 = WindowsKernelModeDriver8.0) 找不到](#what-to-do-if-you-see-error-msb8020)
-   [要执行的操作如果无法将 WDK 8 项目迁移到 WDK 8.1 后生成的 Windows Vista 目标](#build-vista-with-wdk-8-1)

### <span id="What_to_do_if_you_see_Error_MSB8020__Platform_Toolset____WindowsKernelModeDriver8.0___cannot_be_found_"></span><span id="what_to_do_if_you_see_error_msb8020__platform_toolset____windowskernelmodedriver8.0___cannot_be_found_"></span><span id="WHAT_TO_DO_IF_YOU_SEE_ERROR_MSB8020__PLATFORM_TOOLSET____WINDOWSKERNELMODEDRIVER8.0___CANNOT_BE_FOUND_"></span><a name="what-to-do-if-you-see-error-msb8020"></a>要执行的操作如果看到错误 MSB8020 (平台工具集 = WindowsKernelModeDriver8.0) 找不到

如果您尝试打开项目或解决方案，它使用 WDK 8 创建的可能会看到以下错误消息，当你尝试生成使用 WDK 8.1 的项目。

```
1>C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V120\Microsoft.Cpp.Platform.targets(54,5): error MSB8020: The builds tools for WindowsKernelModeDriver8.0 (Platform Toolset = 'WindowsKernelModeDriver8.0') cannot be found. To build using the WindowsKernelModeDriver8.0 build tools, please install WindowsKernelModeDriver8.0 build tools. Alternatively, you may update to the current Visual Studio tools by selecting the Project menu or right-click the solution, and then selecting "Update VC++ Projects...".
```

WDK 8 中的平台工具集已**WindowsKernelModeDriver8.0**。 若要解决此错误，请运行 ProjectUpgradeTool 此处所述，并升级 WDK 8 解决方案以使用 WDK 8.1 中提供的工具集

### <span id="build_vista_with_WDK_8.1"></span><span id="build_vista_with_wdk_8.1"></span><span id="BUILD_VISTA_WITH_WDK_8.1"></span><a name="build-vista-with-wdk-8-1"></a>要执行的操作如果无法将 WDK 8 项目迁移到 WDK 8.1 后生成的 Windows Vista 目标

**问题：** 无法将 WDK 8 项目迁移到 WDK 8.1 后生成的 Windows Vista 目标。

**方案：** 已创建的项目使用 WDK 8 和 Visual Studio 2012。 已升级项目/解决方案使用 WDK 8.1 和 Visual Studio 2013 中，使用 ProjectUpgradeTool 工具。 执行此操作使用以下命令以保留 Windows Vista 配置：**ProjectUpgradeTool.exe** *PathToProjectFolder* **-KeepObsoleteConfigs.**

WDK 8.1 中打开的项目。 生成 Win32 Windows Vista 目标时，可能会看到以下错误消息：

```
error MSB6004: The specified task executable location "C:\Program Files (x86)\Windows Kits\8.0\bin\x86\x86\CL.exe" is invalid.   C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V110\Microsoft.CppCommon.targets  347 5   KMDF Driver1
```

在生成 x64 Windows Vista 的目标，可能会看到以下错误消息：

```
error TRK0002: Failed to execute command: ""C:\Program Files (x86)\Windows Kits\8.0\bin\x64\stampinf.exe" -d * -a amd64 -v * -k 1.11 -u 1.11.0 -f x64\VistaRelease\KMDFDriver1.inf". The operation identifier is not valid.  C:\Users\Administrator\Desktop\KMDF Driver1 - Copy\KMDF Driver1\TRACKER KMDF Driver1
```

```
error : Verification Error: Driver package has no driver version.    C:\Program Files (x86)\Windows Kits\8.0\build\WindowsDriver8.0.common.targets   1338    5   KMDF Driver1 Package
```

**解决方法：** 您需要执行两项更改。

1.  **更正的 WindowsDriver8.0.x64.props 和 WindowsDriver8.0.Win32.props 文件。**

    您需要两个在这些条件表达式中进行的更正\*.props 文件中。 这些文件位于 c： 驱动器中\\Program Files (x86)\\Windows 工具包\\8.0\\生成目录。

    在每个\*.props 文件中，找到表达式其中`('$(VisualStudioVersion)' != '11.0')`。 例如，第一个实例将如以下所示：

    ```XML
            <When  Condition="&#39;$(VisualStudioVersion)&#39; != &#39;11.0&#39;">
          <PropertyGroup>
            <CLToolPath Condition="&#39;$(CLToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86\x64</CLToolPath>
            <CLToolArchitecture>Native32Bit</CLToolArchitecture>
            <LinkToolPath Condition="&#39;$(LinkToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86\x64</LinkToolPath>
            <LinkToolArchitecture>Native32Bit</LinkToolArchitecture>
            <MIDLToolPath Condition="&#39;$(MIDLToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86</MIDLToolPath>
            <MIDLToolArchitecture>Native32Bit</MIDLToolArchitecture>
            <LibToolPath Condition="&#39;$(LibToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86</LibToolPath>
            <LibToolArchitecture>Native32Bit</LibToolArchitecture>
            <ExecutablePath>$(WDKContentRoot)bin\x86\x64;$(WDKContentRoot)bin\x86;$(WDKContentRoot)tools\pfd\bin\bin\AMD64;$(WDKContentRoot)tools\tracing\x64;$(ExecutablePath)</ExecutablePath>      
        </PropertyGroup>
        </When>
    ```

    更改不等于 (！ =) 到小于 ("&lt;")。

    ```XML
        <When  Condition="&#39;$(VisualStudioVersion)&#39; &lt;&#39;11.0&#39;">
    ```

    查找下一个实例，该表达式的位置 `('$(VisualStudioVersion)' != '11.0')`

    ```XML
        <When Condition="(&#39;$(PlatformToolset)&#39; == &#39;WindowsApplicationForDrivers8.0&#39;) and (&#39;$(VisualStudioVersion)&#39; != &#39;11.0&#39;)">
    ```

    和更改不等于 (！ =) 到小于 ("&lt;")。

    ```XML
        <When Condition="(&#39;$(PlatformToolset)&#39; == &#39;WindowsApplicationForDrivers8.0&#39;) and (&#39;$(VisualStudioVersion)&#39; &lt;&#39;11.0&#39;)">
    ```

    进行更改后，将同时保存\*.props 文件中。

2.  **更正该驱动程序的项目文件。**

    打开项目文件 (\*.vcxproj) 为您的驱动程序。

    在项目文件 （发行版和调试） 中找到 Vista 目标配置。 例如：

    ```XML
       <PropertyGroup Label="Configuration" Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Vista Debug|Win32&#39;">
        <TargetVersion>Vista</TargetVersion>
        <UseDebugLibraries>True</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    添加**PackageDir**与 Windows Vista 配置设置的属性。 在大多数情况下，应使用默认值： `<PackageDir>$(OutDir)\$(Intdir)</PackageDir>`。

    ```XML
       <PropertyGroup Label="Configuration" Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Vista Debug|Win32&#39;">
        <TargetVersion>Vista</TargetVersion>
        <PackageDir>$(OutDir)\$(Intdir)</PackageDir>
        <UseDebugLibraries>True</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    进行其他配置的相同的更改。

    ```XML
        <PropertyGroup Label="Configuration" Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Vista Release|Win32&#39;">
        <TargetVersion>Vista</TargetVersion>
        <PackageDir>$(OutDir)\$(Intdir)</PackageDir>
        <UseDebugLibraries>False</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    进行这些更改并保存该文件后可以打开并生成 Visual Studio 2013 中的项目。 项目应继续使用 Visual Studio 2012。 请注意，即使这些更改后仍需要 WDK 8 的计算机上安装 Visual Studio 2012。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[构建一个驱动程序](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)

[WDK 和 Visual Studio 生成环境](wdk-and-visual-studio-build-environment.md)










