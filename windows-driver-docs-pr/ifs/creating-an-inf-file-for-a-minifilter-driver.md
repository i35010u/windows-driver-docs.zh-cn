---
title: 创建筛选器驱动程序的 INF 文件
description: 描述如何创建筛选器驱动程序的 INF 文件
keywords:
- INF 文件系统、微筛选器驱动程序
- INF 文件系统、筛选器驱动程序
- DestinationDirs 节 WDK 文件系统
- 版本部分 WDK 文件系统
- 字符串部分 WDK 文件系统
- ServiceInstall 节 WDK 文件系统
- DefaultInstall 节 WDK 文件系统
- AddRegistry 节 WDK 文件系统
ms.date: 08/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 09f7e318895d911bd1637a1d74fea8cbfd547f10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837279"
---
# <a name="creating-an-inf-file-for-a-filter-driver"></a>创建筛选器驱动程序的 INF 文件

## <a name="introduction"></a>简介

> [!NOTE]
>
> 从 Windows 10 版本1903开始，基元驱动程序的 INF 要求 (例如，) 的文件系统筛选器驱动程序已更改。 有关详细信息，请参阅 [创建新的基元驱动程序](../develop/creating-a-primitive-driver.md) 。

筛选器驱动程序需要在 Windows 操作系统上安装一个 INF 文件。 你将在 [微筛选器示例](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter)中找到示例 INF 文件。

文件系统筛选器驱动程序的 INF 文件通常包含以下部分：

| 部分                       | 说明 |
| -------                       | ----- |
| **Version**                   | 必须 |
| **DestinationDirs**           | 可选，但建议使用 |
| **DefaultInstall**            | 必须 |
| **DefaultInstall**   | 必须 |
| **ServiceInstall**            | 必须 |
| **AddRegistry**               | 必须 |
| **字符串**                   | 必须 |

> [!NOTE]
>
> 从 Windows 10 版本1903开始， **DefaultUninstall** 和 **DefaultUninstall** 部分禁止 [ (异常)](../develop/creating-a-primitive-driver.md#legacy-compatibility)。 这些部分在以前的操作系统版本中是可选的。
>
> Windows 系统64位版本上运行的所有驱动程序都必须在 Windows 加载它们之前进行签名。 有关详细信息，请参阅对 [驱动程序进行签名](../develop/signing-a-driver.md) 。

## <a name="version-section-required"></a>版本部分 (必需) 

[**版本**](../install/inf-version-section.md)部分指定由微筛选器驱动程序类型确定的类和 GUID，如下面的代码示例中所示。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 10/09/2001,1.0.0.0
CatalogFile =
```

下表显示了文件系统微筛选器驱动程序应在 " [**版本**](../install/inf-version-section.md) " 部分中指定的值。

| 条目 | “值” |
| ----- | ----- |
| **Signature** | "$WINDOWS NT $" |
| **类** | 请参阅 [文件系统筛选器驱动程序类和类 guid](file-system-filter-driver-classes-and-class-guids.md)。 |
| **ClassGuid** | 请参阅 [文件系统筛选器驱动程序类和类 guid](file-system-filter-driver-classes-and-class-guids.md)。 |
| **提供程序** | 在你自己的 INF 文件中，你应该指定除 Microsoft 之外的提供程序。 |
| **DriverVer** | 请参阅 [INF DriverVer 指令](../install/inf-driverver-directive.md)。 |
| **CatalogFile** | 对于签名的防病毒微筛选器驱动程序，此条目包含 [WHQL 提供的编录文件](../install/catalog-files.md)的名称。 所有其他微筛选器驱动程序应将此项留空。 有关详细信息，请参阅 [INF 版本部分](../install/inf-version-section.md)中 **CatalogFile** 条目的说明 |

## <a name="destinationdirs-section-optional-but-recommended"></a>DestinationDirs 节 (可选的，但建议使用) 

[**DestinationDirs**](../install/inf-destinationdirs-section.md)部分指定将在其中复制微筛选器驱动程序和应用程序文件的目录。

在此部分和 **ServiceInstall** 节中，你可以按系统定义的数值指定众所周知的系统目录。 有关这些值的列表，请参阅 [INF DestinationDirs 部分](../install/inf-destinationdirs-section.md)。 在下面的代码示例中，值12指驱动程序目录 (% windir% \\ system32 \\ 驱动程序) ，值10引用 Windows 目录 (% windir% ) 。

```cpp
[DestinationDirs]
DefaultDestDir = 12
Minispy.DriverFiles = 12
Minispy.UserFiles   = 10,FltMgr
```

## <a name="defaultinstall-section-required"></a>DefaultInstall 节 (必需的) 

在 [**DefaultInstall**](../install/inf-defaultinstall-section.md) 节中， [**CopyFiles**](../install/inf-copyfiles-directive.md) 指令将微筛选器驱动程序的驱动程序文件和用户应用程序文件复制到 [**DestinationDirs**](../install/inf-destinationdirs-section.md) 节中指定的目标。

> [!NOTE]
>
> [**CopyFiles**](../install/inf-copyfiles-directive.md)指令不应引用目录文件或 INF 文件本身。 Setupapi.log 会自动复制这些文件。

你可以创建一个 INF 文件，用于在多个版本的 Windows 操作系统上安装驱动程序。 可以通过为每个操作系统版本创建附加的 [**DefaultInstall**](../install/inf-defaultinstall-section.md) 和 [**DefaultInstall**](../install/inf-defaultinstall-services-section.md) 部分，创建此类型的 INF 文件。 每节都标记有一个 *修饰* (例如，ntx86、. ntia64 或 nt) ，用于指定应用的操作系统版本。 有关创建此类 INF 文件的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](../install/creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

下面的代码示例演示了一个典型的 [**DefaultInstall**](../install/inf-defaultinstall-section.md) 部分。

```cpp
[DefaultInstall]
OptionDesc = %MinispyServiceDesc%
CopyFiles = Minispy.DriverFiles, Minispy.UserFiles
```

## <a name="defaultinstallservices-section-required"></a>DefaultInstall 节 (必需) 

[**DefaultInstall**](../install/inf-defaultinstall-services-section.md)部分包含的 [**AddService**](../install/inf-addservice-directive.md)指令控制如何以及何时加载特定驱动程序的服务，如下面的代码示例所示。

```cpp
[DefaultInstall.Services]
AddService = %MinispyServiceName%,,Minispy.Service
```

## <a name="serviceinstall-section-required"></a>ServiceInstall 节 (必需的) 

**ServiceInstall** 节包含用于加载驱动程序服务的信息。 在 [MiniSpy 示例驱动程序](/samples/microsoft/windows-driver-samples/minispy-file-system-minifilter-driver/)中，此部分的名称为 "MiniSpy"，如下面的代码示例所示。 **ServiceInstall** 部分的名称必须出现在 [**DefaultInstall**](../install/inf-defaultinstall-services-section.md)部分的 [**AddService**](../install/inf-addservice-directive.md)指令中。

```cpp
[Minispy.Service]
DisplayName    = %MinispyServiceName%
Description    = %MinispyServiceDesc%
ServiceBinary  = %12%\minispy.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL%
LoadOrderGroup = "FSFilter Activity Monitor"
AddReg         = Minispy.AddRegistry
Dependencies   = FltMgr
```

**ServiceType** 条目指定服务的类型。 微筛选器驱动程序应将值指定为 2 (SERVICE_FILE_SYSTEM_DRIVER) 。 有关 **ServiceType** 条目的详细信息，请参阅 [INF AddService 指令](../install/inf-addservice-directive.md)。

**StartType** 项指定启动服务的时间。 下表列出了 **StartType** 的可能值及其相应的启动类型。

| “值”      | 描述 |
| -----      | ----------- |
| 0x00000000 | SERVICE_BOOT_START |
| 0x00000001 | SERVICE_SYSTEM_START |
| 0x00000002 | SERVICE_AUTO_START |
| 0x00000003 | SERVICE_DEMAND_START |
| 0x00000004 | SERVICE_DISABLED |

有关这些启动类型的详细信息，请参阅 [确定驱动程序加载时间的内容](what-determines-when-a-driver-is-loaded.md)中的 "驱动程序启动类型"。

**LoadOrderGroup** 条目为筛选器管理器提供所需的信息，以确保微筛选器驱动程序和旧文件系统筛选器驱动程序之间的互操作性。 应指定一个适用于正在开发的微筛选器驱动程序类型的 **LoadOrderGroup** 值。 若要选择加载顺序组，请参阅 [微筛选器驱动程序的加载顺序组和高度](load-order-groups-and-altitudes-for-minifilter-drivers.md)。

请注意，你必须指定 **LoadOrderGroup** 值，即使你的微筛选器驱动程序的启动类型不 SERVICE_BOOT_START。 通过这种方式，微筛选器驱动程序不同于旧的文件系统筛选器驱动程序。

> [!NOTE]
>
> 筛选器管理器的 **StartType** 值为 SERVICE_BOOT_START，其 **LoadOrderGroup** 值为 FSFilter 基础结构。 这些值可确保在加载任何微筛选器驱动程序之前始终加载筛选器管理器。

有关 **StartType** 和 **LoadOrderGroup** 条目如何确定何时加载驱动程序的详细信息，请参阅 [确定何时加载驱动程序的内容](what-determines-when-a-driver-is-loaded.md)。

对于微筛选器驱动程序，与旧文件系统筛选器驱动程序不同， **StartType** 和 **LoadOrderGroup** 值不确定微筛选器驱动程序在微微筛选器实例堆栈中的位置。 此位置由为微筛选器实例指定的海拔高度决定。

**ErrorControl** 项指定在系统启动过程中服务无法启动时要执行的操作。 微筛选器驱动程序应将值指定为 1 (SERVICE_ERROR_NORMAL) 。 有关 **ErrorControl** 项的详细信息，请参阅 [INF AddService 指令](../install/inf-addservice-directive.md)。

[**AddReg**](../install/inf-addreg-directive.md)指令是指一个或多个 INF 写入器定义的 **AddRegistry** 部分，其中包含要存储在注册表中用于新安装的服务的信息。 微筛选器驱动程序使用 **AddRegistry** 部分来定义微筛选器驱动程序实例，并指定默认实例。

**依赖** 项项指定驱动程序所依赖的任何服务或加载顺序组的名称。 所有微筛选器驱动程序都必须指定 FltMgr，它是筛选器管理器的服务名称。

## <a name="addregistry-section-required"></a>AddRegistry 节 (必需的) 

**AddRegistry** 部分将键和值添加到注册表。 微筛选器驱动程序使用 **AddRegistry** 部分来定义微筛选器实例，并指定默认实例。 筛选器管理器为微筛选器驱动程序创建新的实例时，将使用此信息。

在 [MiniSpy 示例驱动程序](/samples/microsoft/windows-driver-samples/minispy-file-system-minifilter-driver/)中，以下 **AddRegistry** 部分与 [**字符串**](../install/inf-strings-section.md) 部分中的% strkey% token 定义一起定义了三个实例，其中一个实例命名为 MiniSpy 示例驱动程序的默认实例。

```cpp
[Minispy.AddRegistry]
HKR,%RegInstancesSubkeyName%,%RegDefaultInstanceValueName%,0x00000000,%DefaultInstance%
HKR,%RegInstancesSubkeyName%"\"%Instance1.Name%,%RegAltitudeValueName%,0x00000000,%Instance1.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance1.Name%,%RegFlagsValueName%,0x00010001,%Instance1.Flags%
HKR,%RegInstancesSubkeyName%"\"%Instance2.Name%,%RegAltitudeValueName%,0x00000000,%Instance2.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance2.Name%,%RegFlagsValueName%,0x00010001,%Instance2.Flags%
HKR,%RegInstancesSubkeyName%"\"%Instance3.Name%,%RegAltitudeValueName%,0x00000000,%Instance3.Altitude%
HKR,%RegInstancesSubkeyName%"\"%Instance3.Name%,%RegFlagsValueName%,0x00010001,%Instance3.Flags%
```

## <a name="strings-section-required"></a> (必需的字符串部分) 

[**字符串**](../install/inf-strings-section.md)部分定义了在 INF 文件中使用的每个% strkey% 令牌。

可以通过创建其他特定于区域设置的 **字符串** 来创建单个国际 INF 文件。INF 文件中的 *LanguageID* 部分。 有关国际 INF 文件的详细信息，请参阅 [创建国际 Inf 文件](../install/creating-international-inf-files.md)。

下面的代码示例演示了一个典型的 [**字符串**](../install/inf-strings-section.md) 部分。

```cpp
[Strings]
Msft               = "Microsoft Corporation"
MinispyServiceDesc = "Minispy mini-filter driver"
MinispyServiceName = "Minispy"
RegInstancesSubkeyName = "Instances"
RegDefaultInstanceValueName  = "DefaultInstance"
RegAltitudeValueName    = "Altitude"
RegFlagsValueName  = "Flags"

DefaultInstance    = "Minispy - Top Instance"
Instance1.Name     = "Minispy - Middle Instance"
Instance1.Altitude = "370000"
Instance1.Flags    = 0x1 ; Suppress automatic attachments
Instance2.Name     = "Minispy - Bottom Instance"
Instance2.Altitude = "365000"
Instance2.Flags    = 0x1 ; Suppress automatic attachments
Instance3.Name     = "Minispy - Top Instance"
Instance3.Altitude = "385000"
Instance3.Flags    = 0x1 ; Suppress automatic attachments
```

## <a name="defaultuninstall-and-defaultuninstallservices-sections"></a>DefaultUninstall 和 DefaultUninstall 部分

> [!NOTE]
>
> **DefaultUninstall** 和 **DefaultUninstall** 部分禁止 (从 Windows 10 版本1903开始的 [异常)](../develop/creating-a-primitive-driver.md#legacy-compatibility) 。

在1903版之前的 Windows 10 中， **DefaultUninstall** 和 **DefaultUninstall** 部分是可选的，但如果驱动程序可以卸载，则建议使用：

* **DefaultUninstall** 包含 [**DelFiles**](../install/inf-delfiles-directive.md) 和 [**DelReg**](../install/inf-delreg-directive.md) 指令来删除文件和注册表项。
* **DefaultUninstall** 包含 [**DelService**](../install/inf-delservice-directive.md) 指令以删除微筛选器驱动程序的服务。 [**DelService**](../install/inf-delservice-directive.md)指令始终指定 SPSVCINST_STOPSERVICE 标志 (0x00000200) ，以便在服务删除之前停止服务。

下面的示例显示了典型的 **DefaultUninstall** 和 **DefaultUninstall** 节。

```cpp
[DefaultUninstall]
DelFiles   = Minispy.DriverFiles, Minispy.UserFiles
DelReg     = Minispy.DelRegistry

[DefaultUninstall.Services]
DelService = Minispy,0x200
```
