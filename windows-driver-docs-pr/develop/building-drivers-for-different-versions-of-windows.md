---
ms.assetid: 176A3794-E9E9-46C3-B242-422843436D2A
title: 为不同版本的 Windows 生成驱动程序
description: 如果你在为不同版本的 Windows 编写驱动程序，以下部分提供了一些有关如何使用 Windows 驱动程序工具包 (WDK) 8.1 或 WDK 8、Visual Studio 和 MSBuild 生成这些驱动程序的指南。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b485699ff9a7e602ebe2e8d59c49ac7362174b8b
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463938"
---
# <a name="building-drivers-for-different-versions-of-windows"></a>为不同版本的 Windows 生成驱动程序

如果你在[为不同版本的 Windows 编写驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554887)，以下部分提供了一些有关如何使用 Windows 驱动程序工具包 (WDK) 8.1 或 WDK 8、Visual Studio 和 MSBuild 生成这些驱动程序的指南。

## <a name="span-idguidelinesthatapplytobuildingbothuser-modeandkernel-modedriversspanspan-idguidelinesthatapplytobuildingbothuser-modeandkernel-modedriversspanspan-idguidelinesthatapplytobuildingbothuser-modeandkernel-modedriversspanguidelines-that-apply-to-building-both-user-mode-and-kernel-mode-drivers"></a><span id="Guidelines_that_apply_to_building_both_user-mode_and_kernel-mode_drivers"></span><span id="guidelines_that_apply_to_building_both_user-mode_and_kernel-mode_drivers"></span><span id="GUIDELINES_THAT_APPLY_TO_BUILDING_BOTH_USER-MODE_AND_KERNEL-MODE_DRIVERS"></span>用户模式和内核模式驱动程序均适用的生成指南


-   使用 WDK 提供的目标配置和平台生成驱动程序。 应始终使用支持目标 Windows 版本的最新版本的 WDK。 例如，若要为 Windows XP 生成驱动程序，则必须使用 Windows 7 WDK。 但如果要为 Windows 8.1、Windows 8、Windows 7 生成驱动程序，则应使用 WDK 8.1 和 Visual Studio。
-   如果你的驱动程序只能在单个版本的 Windows 上运行，则应为与目标 Windows 版本匹配的目标配置和平台生成驱动程序。 例如，如果正在生成仅在 WDK 8.1 上运行的驱动程序，则应在配置管理器中指定 **Win8.1**。
-   如果希望驱动程序在多个版本的 Windows 上运行，但不使用只有较新版本才提供的功能，则应为你希望驱动程序支持的最旧版本生成驱动程序。 例如，如果你的驱动程序将在从 Windows Vista 开始的所有 Windows 版本上运行，并且它只使用 Windows Vista 上提供的功能，请在项目配置中指定 **Vista**。

## <a name="span-idguidelinesthatapplytobuildingkernel-modedriversspanspan-idguidelinesthatapplytobuildingkernel-modedriversspanspan-idguidelinesthatapplytobuildingkernel-modedriversspanguidelines-that-apply-to-building-kernel-mode-drivers"></a><span id="Guidelines_that_apply_to_building_kernel-mode_drivers"></span><span id="guidelines_that_apply_to_building_kernel-mode_drivers"></span><span id="GUIDELINES_THAT_APPLY_TO_BUILDING_KERNEL-MODE_DRIVERS"></span>内核模式驱动程序适用的生成指南


-   如果希望内核模式驱动程序在多个版本的 Windows 上运行，并且动态确定驱动程序可用的功能，则应使用最新版本操作系统的生成配置生成驱动程序。 例如，如果希望驱动程序支持从 Windows 7 开始的所有 Windows 版本，但在驱动程序运行于 Windows 8.1 或更高版本的操作系统时使用 Windows 8.1 率先推出的某些功能，则应指定 Windows 8.1 (**Win8.1**) 为目标配置。

-   使用 [**RtlIsNtDdiVersionAvailable**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff561954) 和 [**RtlIsServicePackVersionInstalled**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff561956) 函数来确定你的驱动程序在运行时可用的 Windows 版本。 有关详细信息，请参阅[为不同版本的 Windows 编写驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554887)。
-   创建驱动程序必须按条件调用的函数的指针原型。
-   如果你有 WDM 驱动程序或非 KMDF 内核模式驱动程序并且针对 Windows 8.1 或 Windows 8，但同时希望在较早版本的 Windows 上运行，则需要重写链接器 **$(KernelBufferOverflowLib)** 选项。 在选择 Windows 8 或 Windows 8.1 配置时，驱动程序将与 BufferOverflowFastFailK.lib 链接，较早的 Windows 版本中没有这一项。 对于 Windows 7 和 Vista，则必须改为与 BufferOverflowK.lib 链接。

    重写 **$(KernelBufferOverflowLib)** 链接器选项有两种方法：使用 MSBuild 或 Visual Studio。

    **使用 MSBuild：**

    ```cpp
    msbuild /p:KernelBufferOverflowLib="C:\Program Files (x86)\Windows Kits\8.1\Lib\win8\km\x64\BufferOverflowK.lib" /p:platform=x64 /p:Configuration="Win8 Release" myDriver.sln
    ```

    **使用 Visual Studio：**

    使用记事本或其他文本编辑器打开驱动程序项目文件 (\*.vcxproj)。 在项目文件中，找到驱动程序支持的配置的 **&lt;PropertyGroup&gt;**，并添加以下行来重写默认的链接器选项：

    <span codelanguage="XML"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">XML</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> 
       &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
    </code></pre></td>
    </tr>
    </tbody>
    </table>

    例如，如果驱动程序支持 Windows 8.1 和 Windows 8 调试和发布版本，则这些配置部分会如下所示：

    <span codelanguage="XML"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">XML</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>  &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8.1 Debug|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;WindowsV6.3&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;true&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;
      &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8.1 Release|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;WindowsV6.3&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;false&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;
      &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8 Debug|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;Windows8&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;true&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;
      &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8 Release|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;Windows8&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;false&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    **&lt;KernelBufferOverflowLib&gt;** 元素（导入工具集）必须在驱动程序项目文件中显示在导入 Microsoft.Cpp.props 的元素之前。

    修改并保存驱动程序项目文件后，可以在 Visual Studio 中打开该项目文件并生成驱动程序。

## <span id="how_to_customize_target_configuration"></span><span id="HOW_TO_CUSTOMIZE_TARGET_CONFIGURATION"></span>


## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [为不同版本的 Windows 编写驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554887)
* [生成驱动程序](building-a-driver.md)
 

 






