---
title: Windows 驱动程序特定的属性文件
description: 驱动程序属性页将 MSBuild 用于生成任何驱动程序项目的工具的所有默认设置。
ms.assetid: 696EE510-266B-457A-B74E-491D7804B833
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c5c533f07d452e2fdba722b40a6bf1f8607773
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379141"
---
# <a name="span-iddevtestwindowsdriver-specificpropertyfilesspanwindows-driver-specific-property-files"></a><span id="devtest.windows_driver-specific_property_files"></span>Windows 驱动程序特定属性文件


驱动程序属性页将 MSBuild 用于生成任何驱动程序项目的工具的所有默认设置。

下表总结了这些属性表和它们在 MSBuild 用于生成不同的驱动程序的默认设置方面的使用。

**请注意**  在 Windows Driver Kit (WDK) 8，名称的驱动程序属性表文件包含包版本号 (8.0)，例如， **WindowsDriver8.0.KernelMode.ExportDriver.props**。

 

<span id="__WDKContentRoot_"></span><span id="__wdkcontentroot_"></span><span id="__WDKCONTENTROOT_"></span> **$(WDKContentRoot)**  
默认情况下，为在注册表中定义 WDKContentRoot: <strong>$(注册表： HKEY\_本地\_机\\软件\\Microsoft\\Windows 工具包\\WDK@WDKContentRoot)</strong>它指向 * *%programfiles%\\Windows 工具包\\* 版本 * * *。

$(WDKContentRoot)\\生成将有生成扩展插件是为生成驱动程序所需的所有核心。

<span id="WindowsDriver.Default.props"></span><span id="windowsdriver.default.props"></span><span id="WINDOWSDRIVER.DEFAULT.PROPS"></span>**WindowsDriver.Default.props**  
定义使用的任何驱动程序的版本控制常量。 例如，  **&lt; \_NT\_目标\_版本\_WIN7&gt;0x0601&lt;/\_NT\_目标\_版本\_WIN7&gt;** 。

<span id="WindowsDriver.Common.props"></span><span id="windowsdriver.common.props"></span><span id="WINDOWSDRIVER.COMMON.PROPS"></span>**WindowsDriver.Common.props**  
生成所有驱动程序的内核模式和用户模式下所需的常见设置。

<span id="WindowsDriver.Shared.props"></span><span id="windowsdriver.shared.props"></span><span id="WINDOWSDRIVER.SHARED.PROPS"></span>**WindowsDriver.Shared.props**  
此属性文件包含生成应用程序，以及一个驱动程序所需的共享的生成设置。 在所有 WDK 工具集，例如，WindowsKernelModeDriver8.1、 WindowsUserModeDriver8.1 和 WindowsApplicationForDrivers8.1 中都使用此文件。

<span id="WindowsDriver.__Platform_.props"></span><span id="windowsdriver.__platform_.props"></span><span id="WINDOWSDRIVER.__PLATFORM_.PROPS"></span>**WindowsDriver。 $（平台）.props**  
这些设置是通用 MSBuild 应用根据目标体系结构的驱动程序设置。 **$（平台） = Win32 | x64**

<span id="WindowsDriver.KernelMode.props"></span><span id="windowsdriver.kernelmode.props"></span><span id="WINDOWSDRIVER.KERNELMODE.PROPS"></span>**WindowsDriver.KernelMode.props**  
此属性文件包含生成任何内核模式二进制所需的常见设置。 换而言之，这些设置不适用于用户模式驱动程序和应用程序。

<span id="WindowsDriver.KernelMode.Driver.props"></span><span id="windowsdriver.kernelmode.driver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.DRIVER.PROPS"></span>**WindowsDriver.KernelMode.Driver.props**  
此属性文件导入特定的内核模式驱动程序类型属性文件 (例如，WindowsDriver.8.1.KernelMode.KMDF.props)

<span id="WindowsDriver.KernelMode.KMDF.props"></span><span id="windowsdriver.kernelmode.kmdf.props"></span><span id="WINDOWSDRIVER.KERNELMODE.KMDF.PROPS"></span>**WindowsDriver.KernelMode.KMDF.props**  
这些属性设置包含需要应用仅当要构建 KMDF 驱动程序时的特殊设置。 使用 MSBuild **$(DriverType)** 属性指定的驱动程序类型**KMDF**，如下面的示例： *&lt;DriverType&gt;KMDF&lt;/DriverType&gt;*

<span id="WindowsDriver.KernelMode.Wdm.props"></span><span id="windowsdriver.kernelmode.wdm.props"></span><span id="WINDOWSDRIVER.KERNELMODE.WDM.PROPS"></span>**WindowsDriver.KernelMode.Wdm.props**  
这些属性设置包含需要仅在生成 WDM 驱动程序时应用的特殊设置。 使用 MSBuild **$(DriverType)** 属性指定的驱动程序类型**WDM**，如下面的示例： *&lt;DriverType&gt;wdm&lt;/DriverType&gt;* 。

<span id="WindowsDriver.KernelMode.Gdidriver.props"></span><span id="windowsdriver.kernelmode.gdidriver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.GDIDRIVER.PROPS"></span>**WindowsDriver.KernelMode.Gdidriver.props**  
这些属性设置包含需要仅在生成 GDI 驱动程序时应用的特殊设置。 使用 MSBuild **$(DriverType)** 属性指定的驱动程序类型**Gdidriver**，如下面的示例： *&lt;DriverType&gt;Gdidriver&lt;/DriverType&gt;* 。

<span id="WindowsDriver.KernelMode.ExportDriver.props"></span><span id="windowsdriver.kernelmode.exportdriver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.EXPORTDRIVER.PROPS"></span>**WindowsDriver.KernelMode.ExportDriver.props**  
这些属性设置包含需要时才应用正在生成导出驱动程序的特殊设置。 使用 MSBuild **$(DriverType)** 属性指定的驱动程序类型**ExportDriver**，如下面的示例： *&lt;DriverType&gt;ExportDriver&lt;/DriverType&gt;* 。

<span id="WindowsDriver.KernelMode.Miniport.props"></span><span id="windowsdriver.kernelmode.miniport.props"></span><span id="WINDOWSDRIVER.KERNELMODE.MINIPORT.PROPS"></span>**WindowsDriver.KernelMode.Miniport.props**  
这些属性设置是生成微型端口驱动程序时必须应用的特殊设置。 使用 MSBuild **$(DriverType)** 属性指定驱动程序类型为**微型端口**，如下面的示例： *&lt;DriverType&gt;微型端口&lt;/DriverType&gt;* 。

<span id="WindowsDriver.LateEvaluation.props_"></span><span id="windowsdriver.lateevaluation.props_"></span><span id="WINDOWSDRIVER.LATEEVALUATION.PROPS_"></span>**WindowsDriver.LateEvaluation.props**   
仅限内部使用。 不要编辑或使用。

<span id="WindowsDriver.masm.props"></span><span id="windowsdriver.masm.props"></span><span id="WINDOWSDRIVER.MASM.PROPS"></span>**WindowsDriver.masm.props**  
这些属性设置用于生成程序集文件 (MASM) 的支持的体系结构 （平台） 中包含的设置。

<span id="WindowsDriver.UserMode.props"></span><span id="windowsdriver.usermode.props"></span><span id="WINDOWSDRIVER.USERMODE.PROPS"></span>**WindowsDriver.UserMode.props**  
这些属性设置是生成仅任何用户模式驱动程序所需的常见设置。 换而言之，不适用于这些内核模式驱动程序和应用程序的设置。

<span id="WindowsDriver.UserMode.UMDF"></span><span id="windowsdriver.usermode.umdf"></span><span id="WINDOWSDRIVER.USERMODE.UMDF"></span>**WindowsDriver.UserMode.UMDF**  
这些属性设置是生成 UMDF 驱动程序时必须应用的特殊设置。 使用 MSBuild **$(DriverType)** 属性指定的驱动程序类型**UMDF**，如下面的示例： *&lt;DriverType&gt;UMDF&lt;/DriverType&gt;* 。

 

 





