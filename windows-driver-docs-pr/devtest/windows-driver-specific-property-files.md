---
title: Windows 驱动程序特定的属性文件
description: "\"驱动程序\" 属性表具有 MSBuild 用于生成任何驱动程序项目的所有工具的默认设置。"
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8038cd63104448ebda2ceb25e01faeab7f6daadd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810668"
---
# <a name="span-iddevtestwindows_driver-specific_property_filesspanwindows-driver-specific-property-files"></a><span id="devtest.windows_driver-specific_property_files"></span>Windows 驱动程序特定的属性文件


"驱动程序" 属性表具有 MSBuild 用于生成任何驱动程序项目的所有工具的默认设置。

下表汇总了这些属性表，并按 MSBuild 用于构建不同驱动程序的默认设置进行了说明。

**注意**  在 Windows 驱动程序工具包 (WDK) 8 中，驱动程序属性表文件的名称包含包版本号 (8.0) ，例如 **Windowsdriver KernelMode. ExportDriver. 属性**。

 

<span id="__WDKContentRoot_"></span><span id="__wdkcontentroot_"></span><span id="__WDKCONTENTROOT_"></span>**$ (WDKContentRoot)**  
默认情况下，会在注册表中将 WDKContentRoot 定义为： <strong>$ (注册表： HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ windows 工具包， \\ WDK@WDKContentRoot)</strong>指向 **% programfiles% \\ Windows \\ 工具包* 版本 * * *。

$ (WDKContentRoot) \\ 生成将具有构建驱动程序所需的所有核心生成扩展。

<span id="WindowsDriver.Default.props"></span><span id="windowsdriver.default.props"></span><span id="WINDOWSDRIVER.DEFAULT.PROPS"></span>**WindowsDriver. 属性**  
定义任何驱动程序所用的版本控制常数。 例如， **&lt; \_ nt \_ target \_ 版本 \_ win7 &gt; 0x0601 &lt; / \_ nt \_ 目标 \_ 版本 \_ win7 &gt;**。

<span id="WindowsDriver.Common.props"></span><span id="windowsdriver.common.props"></span><span id="WINDOWSDRIVER.COMMON.PROPS"></span>**WindowsDriver. 属性**  
构建所有驱动程序所需的常见设置-内核模式和用户模式。

<span id="WindowsDriver.Shared.props"></span><span id="windowsdriver.shared.props"></span><span id="WINDOWSDRIVER.SHARED.PROPS"></span>**WindowsDriver. 属性**  
此属性文件包含生成应用程序和驱动程序所需的共享生成设置。 此文件用于所有 WDK 工具集，例如 WindowsKernelModeDriver 8.1、WindowsUserModeDriver 8.1 和 WindowsApplicationForDrivers 8.1。

<span id="WindowsDriver.__Platform_.props"></span><span id="windowsdriver.__platform_.props"></span><span id="WINDOWSDRIVER.__PLATFORM_.PROPS"></span>**WindowsDriver. $ (平台) . 属性**  
这些设置是 MSBuild 根据目标体系结构应用的常见驱动程序设置。 **$ (平台) = Win32 | x64**

<span id="WindowsDriver.KernelMode.props"></span><span id="windowsdriver.kernelmode.props"></span><span id="WINDOWSDRIVER.KERNELMODE.PROPS"></span>**WindowsDriver. KernelMode. 属性**  
此属性文件包含仅生成任何内核模式二进制文件所需的常见设置。 换句话说，这些设置不适用于用户模式驱动程序和应用程序。

<span id="WindowsDriver.KernelMode.Driver.props"></span><span id="windowsdriver.kernelmode.driver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.DRIVER.PROPS"></span>**WindowsDriver. KernelMode. 属性**  
此属性文件导入特定的内核模式驱动程序类型属性文件 (例如，WindowsDriver) 

<span id="WindowsDriver.KernelMode.KMDF.props"></span><span id="windowsdriver.kernelmode.kmdf.props"></span><span id="WINDOWSDRIVER.KERNELMODE.KMDF.PROPS"></span>**WindowsDriver. KernelMode. KMDF. 属性**  
这些属性设置包含只有在生成 KMDF 驱动程序时才必须应用的特殊设置。 MSBuild 使用 **$ (DriverType)** 属性将驱动程序类型指定为 **KMDF**，如以下示例中所示： *&lt; DriverType &gt; KMDF &lt; /DriverType &gt;*

<span id="WindowsDriver.KernelMode.Wdm.props"></span><span id="windowsdriver.kernelmode.wdm.props"></span><span id="WINDOWSDRIVER.KERNELMODE.WDM.PROPS"></span>**WindowsDriver. KernelMode. 属性**  
这些属性设置包含只有在生成 WDM 驱动程序时才必须应用的特殊设置。 MSBuild 使用 **$ (DriverType)** 属性将驱动程序类型指定为 **WDM**，如以下示例中所示： *&lt; DriverType &gt; WDM &lt; /DriverType &gt;*。

<span id="WindowsDriver.KernelMode.Gdidriver.props"></span><span id="windowsdriver.kernelmode.gdidriver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.GDIDRIVER.PROPS"></span>**WindowsDriver. KernelMode. Gdidriver. 属性**  
这些属性设置包含只有在生成 GDI 驱动程序时才必须应用的特殊设置。 MSBuild 使用 **$ (DriverType)** 属性将驱动程序类型指定为 **Gdidriver**，如以下示例中所示： *&lt; DriverType &gt; Gdidriver &lt; /DriverType &gt;*。

<span id="WindowsDriver.KernelMode.ExportDriver.props"></span><span id="windowsdriver.kernelmode.exportdriver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.EXPORTDRIVER.PROPS"></span>**WindowsDriver. KernelMode. ExportDriver. 属性**  
这些属性设置包含只有在生成导出驱动程序时才必须应用的特殊设置。 MSBuild 使用 **$ (DriverType)** 属性将驱动程序类型指定为 **ExportDriver**，如以下示例中所示： *&lt; DriverType &gt; ExportDriver &lt; /DriverType &gt;*。

<span id="WindowsDriver.KernelMode.Miniport.props"></span><span id="windowsdriver.kernelmode.miniport.props"></span><span id="WINDOWSDRIVER.KERNELMODE.MINIPORT.PROPS"></span>**WindowsDriver. KernelMode. 属性**  
这些属性设置是在生成微型端口驱动程序时必须应用的特殊设置。 MSBuild 使用 **$ (DriverType)** 属性将驱动程序类型指定为 **微型端口**，如以下示例中所示： *&lt; DriverType &gt; 微型端口 &lt; /DriverType &gt;*。

<span id="WindowsDriver.LateEvaluation.props_"></span><span id="windowsdriver.lateevaluation.props_"></span><span id="WINDOWSDRIVER.LATEEVALUATION.PROPS_"></span>**WindowsDriver. LateEvaluation. 属性**   
仅限内部使用。 请勿编辑或使用。

<span id="WindowsDriver.masm.props"></span><span id="windowsdriver.masm.props"></span><span id="WINDOWSDRIVER.MASM.PROPS"></span>**WindowsDriver. 属性**  
这些属性设置包含用于构建程序集文件 (MASM) 的设置， (平台) 支持的体系结构。

<span id="WindowsDriver.UserMode.props"></span><span id="windowsdriver.usermode.props"></span><span id="WINDOWSDRIVER.USERMODE.PROPS"></span>**WindowsDriver. UserMode. 属性**  
这些属性设置是仅生成任何用户模式驱动程序所需的常见设置。 换句话说，不要将这些设置应用于内核模式驱动程序和应用程序。

<span id="WindowsDriver.UserMode.UMDF"></span><span id="windowsdriver.usermode.umdf"></span><span id="WINDOWSDRIVER.USERMODE.UMDF"></span>**WindowsDriver. UserMode**  
这些属性设置是在生成 UMDF 驱动程序时必须应用的特殊设置。 MSBuild 使用 **$ (DriverType)** 属性将驱动程序类型指定为 **UMDF**，如以下示例中所示： *&lt; DriverType &gt; UMDF &lt; /DriverType &gt;*。

 

 





