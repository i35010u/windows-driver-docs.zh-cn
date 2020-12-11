---
title: 驱动程序项目的驱动程序模型设置属性
description: 为内核模式或用户模式驱动程序设置基本属性，包括 WDF 库版本和预处理器定义。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a054d971ee3da9d789207c7b3bdacb4d9797d20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838809"
---
# <a name="driver-model-settings-properties-for-driver-projects"></a>驱动程序项目的驱动程序模型设置属性

为内核模式或用户模式驱动程序设置基本属性，包括 WDF 库版本和预处理器定义。

## <a name="setting-driver-model-properties-for-driver-projects"></a>设置驱动程序项目的驱动程序模型属性


1.  打开驱动程序项目的属性页。 在“解决方案资源管理器”中，选择并按住（或右键单击）驱动程序项目，然后选择“属性” 。
2.  在驱动程序项目的属性页中，选择“配置属性”，然后选择“驱动程序模型设置” 。
3.  设置项目属性。

**驱动程序的类型**  
**配置类型** 为“驱动程序”  时的驱动程序的类型。 请注意，仅当项目使用 **WindowsKernelModeDriver8.0** 工具集时此选项才可用。

可能的值为：

* **WDM**（包括所有微型端口/端口驱动程序，如 NDIS 或 StorPort）。
* **KMDF** 一个 KMDF 驱动程序。
* **导出驱动程序 (WDM)** 导出其他驱动程序可调用的函数的 WDM 驱动程序。 有关详细信息，请参阅[创建导出驱动程序](../kernel/creating-export-drivers.md)。

**KMDF 主要版本**  
当驱动程序类型为 KMDF 时，此选项指定编译驱动程序时将使用的 KMDF 的主要版本。

KMDF\_VERSION\_MAJOR 条目通知 MSBuild 实用工具必须将驱动程序链接到 KMDF 库。

有关详细信息，请参阅[框架库版本控制](../wdf/framework-library-versioning.md)。

**KMDF 次要版本(目标版本)** （为 Windows 10 版本 1803 之前的 **KMDF 次要版本**）当驱动程序类型为 KMDF 时，此选项指定编译驱动程序时将使用的 KMDF 次要版本。

有关详细信息，请参阅[框架库版本控制](../wdf/framework-library-versioning.md)。 如果你没有指定“KMDF 次要版本(目标版本)”  ，则 Visual Studio 将使用以下默认值：
* Windows 10：1.15
* Windows 8/Windows 8.1：1.11
* Windows 7：1.9

**KMDF 次要版本(最低要求)** （可选，从 Windows 10 版本 1803 开始提供）从 Windows 10 版本 1803 (Redstone 4) 上的 KMDF 版本 1.25 和 UMDF 版本 2.25 开始，你可以构建一个面向一系列框架版本的 KMDF 驱动程序。 使用此可选设置指定此范围的最低 KMDF 版本。

有关详细信息，请参阅[针对多个 Windows 版本构建 WDF 驱动程序](../wdf/building-a-wdf-driver-for-multiple-versions-of-windows.md)。

**UMDF 主要版本**  
当你有 UMDF 驱动程序时，此选项指定编译驱动程序时将使用的 UMDF 的主要版本。 请参阅 [UMDF 版本历史记录](../wdf/umdf-version-history.md)。 当你有 UMDF 驱动程序时，**配置类型** 为“动态库(.dll)”  。

**UMDF 次要版本(目标版本)** （为 Windows 10 版本 1803 之前的 **UMDF 次要版本**）当你有 UMDF 驱动程序时，此选项指定编译驱动程序时将使用的 UMDF 次要版本。 如果你没有指定“UMDF 次要版本(目标版本)”  ，则 Visual Studio 将使用以下默认值：

对于主要版本 = 2：
* Windows 10：2.15
* 其他：2.0

对于主要版本 = 1：
* Windows 8 和更高版本：1.11
* Windows 7：1.9

**UMDF 次要版本(最低要求)** （可选，从 Windows 10 版本 1803 开始提供）

从 Windows 10 版本 1803 (Redstone 4) 上的 KMDF 版本 1.25 和 UMDF 版本 2.25 开始，你可以构建一个面向一系列框架版本的 UMDF 驱动程序。 使用此可选设置指定此范围的最低 UMDF 版本。

有关详细信息，请参阅[针对多个 Windows 版本构建 WDF 驱动程序](../wdf/building-a-wdf-driver-for-multiple-versions-of-windows.md)。

**允许日期、时间和时间戳**  
为 \_\_DATE\_\_、\_\_TIME\_\_、\_\_TIMESTAMP\_\_ 定义标准 C/CPP 宏。

**替代目标配置预处理器定义**  
替代预处理符号的默认值：源文件的 \_WIN32\_WINNT、WINVER、WINNT 和 NTDDI\_VERSION。 请注意，默认值由当前的目标配置控制。

## <a name="related-topics"></a>相关主题


* [框架库版本控制](../wdf/framework-library-versioning.md)
* [生成并加载基于框架的驱动程序](../wdf/building-and-loading-a-kmdf-driver.md)
* [UMDF 版本历史记录](../wdf/umdf-version-history.md)
* [生成 UMDF 驱动程序](../wdf/building-and-loading-a-kmdf-driver.md)
* [创建导出驱动程序](../kernel/creating-export-drivers.md)
 

