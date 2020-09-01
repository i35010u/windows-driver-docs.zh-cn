---
title: 为文件系统驱动程序创建 INF 文件
description: 为文件系统驱动程序创建 INF 文件
ms.assetid: 4b67159f-a5a5-46da-9500-a9c6b6995da4
keywords:
- INF 文件系统，创建
- Setupapi.log WDK 文件系统
- 字符串部分 WDK 文件系统
- DefaultUninstall 节 WDK 文件系统
- ServiceInstall 节 WDK 文件系统
- DefaultInstall 节 WDK 文件系统
- SourceDisksNames 节 WDK 文件系统
- DestinationDirs 节 WDK 文件系统
- 版本部分 WDK 文件系统
- 创建 INF 文件系统
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1bb397095863bd092a463eacdc644ff1cd6db117
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065102"
---
# <a name="creating-an-inf-file-for-a-file-system-driver"></a>为文件系统驱动程序创建 INF 文件

Windows 安装程序和设备安装程序服务（统称为 [setupapi.log](../install/setupapi.md)）提供控制 Windows 安装程序和驱动程序安装的功能。 安装过程由 INF 文件控制。

文件系统驱动程序的 INF 文件提供 Setupapi.log 用于安装驱动程序的说明。 INF 文件是一个文本文件，该文件指定要运行的驱动程序必须存在的文件，以及驱动程序文件的源和目标目录。 INF 文件还包含 Setupapi.log 存储在注册表中的驱动程序配置信息，如驱动程序的启动类型和加载顺序组。

有关 INF 文件及其创建方式的详细信息，请参阅 [创建 Inf 文件](../install/overview-of-inf-files.md) 和 [inf 文件部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。 有关签名驱动程序的常规信息，请参阅 [驱动程序签名](../install/driver-signing.md)。

你可以创建一个 INF 文件，用于在多个版本的 Windows 操作系统上安装驱动程序。 有关创建此类 INF 文件的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](../install/creating-inf-files-for-multiple-platforms-and-operating-systems.md) 和 [创建国际 INF 文件](../install/creating-international-inf-files.md)。

从64位版本的 Windows Vista 开始，所有内核模式组件（包括非 PnP (即插即用) 驱动程序（如文件系统驱动程序 (文件系统、旧筛选器和微筛选器驱动) 程序）都必须经过签名才能加载和执行。 对于这些版本的 Windows 操作系统，下表包含与文件系统驱动程序相关的信息。

- 非 PnP 驱动程序的 INF 文件（包括文件系统驱动程序）不需要包含 \[ 制造商 \] 或 \[ 型号 \] 部分。

- 位于 WDK 安装目录的 \bin\SelfSign 目录中的 [**SignTool**](../devtest/signtool.md) 命令行工具可用于直接 "嵌入签名" 驱动程序的可执行文件。 出于性能方面的考虑，启动驱动程序必须包含一个嵌入签名。

- 给定一个 INF 文件后，可以使用 [**Inf2Cat**](../devtest/inf2cat.md) 命令行工具为驱动程序包创建编录 ( 类) 文件。 只有目录文件才能接收 [WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705) 徽标签名。

- 使用管理员权限时，仍可以在从 Windows Vista 开始的基于 x64 的系统上安装未签名的驱动程序。 但是，驱动程序将无法加载 (，因此执行) ，因为它是无符号的。

- 有关驱动签名过程的详细信息，包括适用于64位版本的 Windows Vista 的驱动签名过程，请参阅 [内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

- 所有内核模式组件（包括自定义内核模式开发工具）都必须经过签名。 有关详细信息，请参阅 [在开发和测试期间对驱动程序进行签名 (Windows Vista 和更高版本) ](../install/introduction-to-test-signing.md)。

INF 文件不能用于从注册表读取信息或启动用户模式应用程序。

创建 INF 文件后，通常会为安装应用程序编写源代码。 安装应用程序调用用户模式安装程序功能来访问 INF 文件中的信息并执行安装操作。

若要构造自己的文件系统驱动程序 INF 文件，请使用以下信息作为指南。 可以使用 [InfVerif](../devtest/infverif.md) 工具来检查 INF 文件的语法。

文件系统驱动程序的 INF 文件通常包含以下各节。

- 需要 (版本) 

- DestinationDirs (可选的，但建议使用) 

- SourceDisksNames (必需) 

- SourceDisksFiles (必需) 

- DefaultInstall (必需) 

- DefaultInstall (必需) 

- ServiceInstall (必需) 

- DefaultUninstall (可选) 

- DefaultUninstall (可选) 

- 字符串 (必需) 

### <a name="version-section-required"></a>版本部分 (必需) 

[**版本**](../install/inf-version-section.md)部分指定驱动程序版本信息，如下面的代码示例中所示。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Provider    = %Msft%
DriverVer   = 08/28/2000,1.0.0.1
CatalogFile =
```

下表显示文件系统筛选器驱动程序在 " [**版本**](../install/inf-version-section.md) " 部分中应指定的值。

| 条目 | 值 |
| ----- | ----- |
| **信号** | "$WINDOWS NT $" |
| **提供程序** | 在你自己的 INF 文件中，你应该指定除 Microsoft 之外的提供程序。 |
| **DriverVer** | 请参阅[ **INF DriverVer 指令**](../install/inf-driverver-directive.md) |
| **CatalogFile** | 将此项留空。 将来，它将包含已签名驱动程序的 WHQL 提供的编录文件的名称。 |

### <a name="destinationdirs-section-optional-but-recommended"></a>DestinationDirs 节 (可选的，但建议使用) 

[**DestinationDirs**](../install/inf-destinationdirs-section.md)节指定将在其中复制文件系统驱动程序文件的目录。

在此部分和 **ServiceInstall** 节中，你可以通过使用系统定义的数值来指定众所周知的系统目录。 有关这些值的列表，请参阅 [**INF DestinationDirs 部分**](../install/inf-destinationdirs-section.md)。 在下面的代码示例中，值 "12" 指的是 (%windir%\system32\drivers) 的驱动程序目录。

```cpp
[DestinationDirs]
DefaultDestDir = 12
ExampleFileSystem.DriverFiles = 12
```

### <a name="sourcedisksnames-section-required"></a>SourceDisksNames 节 (必需的) 

[**SourceDisksNames**](../install/inf-sourcedisksnames-section.md)部分指定要使用的分发媒体。

在下面的代码示例中， [**SourceDisksNames**](../install/inf-sourcedisksnames-section.md) 部分列出了文件系统驱动程序的单个分发媒体。 媒体的唯一标识符是1。 媒体的名称由% Disk1% 令牌指定，该令牌在 INF 文件的 **字符串** 部分中定义。

```cpp
[SourceDisksNames]
1 = %Disk1%
```

### <a name="sourcedisksfiles-section-required"></a>SourceDisksFiles 节 (必需的) 

[**SourceDisksFiles**](../install/inf-sourcedisksfiles-section.md)部分指定要复制的文件的位置和名称。

在下面的代码示例中， [**SourceDisksFiles**](../install/inf-sourcedisksfiles-section.md) 部分列出了要为文件系统驱动程序复制的文件，并指定文件可以在其唯一标识符为 1 (在 INF 文件的 [**SourceDisksNames**](../install/inf-sourcedisksnames-section.md) 部分定义此标识符的介质中找到。 ) 

```cpp
[SourceDisksFiles]
examplefilesystem.sys = 1
```

### <a name="defaultinstall-section-required"></a>DefaultInstall 节 (必需的) 

在 [**DefaultInstall**](../install/inf-defaultinstall-section.md) 节中， [**CopyFiles**](../install/inf-copyfiles-directive.md) 指令将文件系统驱动程序的驱动程序文件复制到 [**DestinationDirs**](../install/inf-destinationdirs-section.md) 节中指定的目标。

> [!NOTE]
> [**CopyFiles**](../install/inf-copyfiles-directive.md)指令不应引用目录文件或 INF 文件本身;Setupapi.log 会自动复制这些文件。

你可以创建一个 INF 文件，用于在多个版本的 Windows 操作系统上安装驱动程序。 通过为每个操作系统版本创建附加的 [**DefaultInstall**](../install/inf-defaultinstall-section.md)、 [**DefaultInstall**](../install/inf-defaultinstall-services-section.md)、 **DefaultUninstall**和 **DefaultUninstall** 节来创建这种类型的 INF 文件。 每节都标记有一个 *修饰* (例如，ntx86、. ntia64 或 nt) ，用于指定应用的操作系统版本。 有关创建此类 INF 文件的详细信息，请参阅 [为多个平台和操作系统创建 INF 文件](../install/creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

在下面的代码示例中， [**CopyFiles**](../install/inf-copyfiles-directive.md) 指令复制在 INF 文件的 ExampleFileSystem. DriverFiles 节中列出的文件。

```cpp
[DefaultInstall]
OptionDesc = %ServiceDesc%
CopyFiles = ExampleFileSystem.DriverFiles

[ExampleFileSystem.DriverFiles]
examplefilesystem.sys
```

### <a name="defaultinstallservices-section-required"></a>DefaultInstall 节 (必需) 

[**DefaultInstall**](../install/inf-defaultinstall-services-section.md)部分包含的[**AddService**](../install/inf-addservice-directive.md)指令控制如何以及何时加载特定驱动程序的服务。

在下面的代码示例中， [**AddService**](../install/inf-addservice-directive.md) 指令将文件系统服务添加到操作系统。 % ServiceName% 令牌包含在 INF 文件的 **字符串** 部分中定义的服务名称字符串。 ExampleFileSystem 是文件系统驱动程序的 **ServiceInstall** 节的名称。

```cpp
[DefaultInstall.Services]
AddService = %ServiceName%,,ExampleFileSystem.Service
```

### <a name="serviceinstall-section-required"></a>ServiceInstall 节 (必需的) 

**ServiceInstall**节将子项或值名称添加到注册表中，并设置值。 **ServiceInstall**部分的名称必须出现在[**DefaultInstall 部分**](../install/inf-defaultinstall-services-section.md)的[**AddService 指令**](../install/inf-addservice-directive.md)中。

下面的代码示例显示了文件系统驱动程序的 **ServiceInstall** 部分。

```cpp
[ExampleFileSystem.Service]
DisplayName    = %ServiceName%
Description    = %ServiceDesc%
ServiceBinary  = %12%\examplefilesystem.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 1 ;    SERVICE_SYSTEM_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL
LoadOrderGroup = "File System"
AddReg         = ExampleFileSystem.AddRegistry
```

**DisplayName**项指定服务的名称。 在前面的示例中，服务名称字符串由% ServiceName% 令牌指定，该令牌在 INF 文件的 **字符串** 部分中定义。

**Description**条目指定描述服务的字符串。 在前面的示例中，此字符串由% ServiceDesc% 令牌指定，该令牌在 INF 文件的 **字符串** 部分中定义。

**ServiceBinary**项指定服务的可执行文件的路径。 在前面的示例中，值12指的是驱动程序目录 (%windir%\system32\drivers) 。

**ServiceType**条目指定服务的类型。 下表列出了 **ServiceType** 的可能值及其相应的服务类型。

| 值 | 说明 |
| ----- | ----------- |
| 0x00000001 |  (设备驱动程序服务 SERVICE_KERNEL_DRIVER)  |
| 0x00000002 | SERVICE_FILE_SYSTEM_DRIVER (文件系统或文件系统筛选器驱动程序服务)  |
| 0x00000010 | SERVICE_WIN32_OWN_PROCESS (Microsoft Win32 服务，该服务在其自己的进程中运行)  |
| 0x00000020 | 共享进程 (Win32 服务 SERVICE_WIN32_SHARE_PROCESS)  |

对于文件系统驱动程序， **ServiceType** 条目应始终设置为 SERVICE_FILE_SYSTEM_DRIVER。

**StartType**项指定启动服务的时间。 下表列出了 **StartType** 的可能值及其相应的启动类型。

| 值 | 说明 |
| ----- | ----------- |
| 0x00000000 | SERVICE_BOOT_START |
| 0x00000001 | SERVICE_SYSTEM_START |
| 0x00000002 | SERVICE_AUTO_START |
| 0x00000003 | SERVICE_DEMAND_START |
| 0x00000004 | SERVICE_DISABLED |

有关这些启动类型的详细说明，以确定哪种类型适合你的文件系统驱动程序，请参阅 [确定何时加载驱动程序的内容](what-determines-when-a-driver-is-loaded.md)。

从基于 x64 的 Windows Vista 系统开始，启动驱动程序的二进制映像文件 (启动类型 SERVICE_BOOT_START) 的驱动程序必须包含嵌入签名。 此要求可确保系统的最佳启动性能。 有关详细信息，请参阅 [内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

有关 **StartType** 和 **LoadOrderGroup** 条目如何确定何时加载驱动程序的信息，请参阅 [确定何时加载驱动程序的内容](what-determines-when-a-driver-is-loaded.md)。

**ErrorControl**项指定在系统启动过程中服务无法启动时要执行的操作。 下表列出了 **ErrorControl** 的可能值及其相应的错误控制值。

| 值 | 说明 |
| ----- | ----------- |
| 0x00000000 | SERVICE_ERROR_IGNORE (记录错误并继续系统启动。 )  |
| 0x00000001 | SERVICE_ERROR_NORMAL (记录错误、向用户显示一条消息，然后继续系统启动。 )  |
| 0x00000002 | SERVICE_ERROR_SEVERE (切换到注册表的 LastKnownGood 控件集，然后继续系统启动。 |
| 0x00000003 | SERVICE_ERROR_CRITICAL (如果系统启动未使用注册表的 LastKnownGood 控制集，请切换到 LastKnownGood 并重试。 如果启动仍然失败，请运行 bug 检查例程。 只有系统启动所需的驱动程序才能在其 INF 文件中指定此值。 )  |

对于文件系统驱动程序， **LoadOrderGroup** 条目必须始终设置为 "文件系统"。 这不同于为文件系统筛选器驱动程序或文件系统微筛选器驱动程序指定的，其中 **LoadOrderGroup** 项设置为其中一个文件系统筛选器加载顺序组。 有关用于文件系统筛选器驱动程序和文件系统微筛选器驱动程序的加载顺序组的详细信息，请参阅用于 [文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md) 和 [加载顺序组以及微筛选器驱动程序的高度](load-order-groups-and-altitudes-for-minifilter-drivers.md)。

[**AddReg 指令**](../install/inf-addreg-directive.md)是指一个或多个 INF 写入器定义的**AddRegistry**部分，其中包含要存储在注册表中用于新安装的服务的任何信息。

**注意**   如果在初始安装后 INF 文件还将用于升级驱动程序，则在**AddRegistry**节中包含的条目应 FLG_ADDREG_NOCLOBBER) 标志指定 0x00000002 (。 如果指定此标志，则在安装后续文件时，会保留 HKLM\CurrentControlSet\Services 中的注册表项。 例如：

```cpp
[ExampleFileSystem.AddRegistry]
HKR,Parameters,ExampleParameter,0x00010003,1
```

### <a name="defaultuninstall-section-optional"></a>DefaultUninstall 节 (可选) 

**DefaultUninstall**节是可选的，但如果你的驱动程序可以卸载，则建议使用。 它包含 [**DelFiles**](../install/inf-delfiles-directive.md) 和 [**DelReg**](../install/inf-delreg-directive.md) 指令以删除文件和注册表项。

在下面的代码示例中， [**DelFiles**](../install/inf-delfiles-directive.md) 指令会删除 INF 文件的 ExampleFileSystem. DriverFiles 节中列出的文件。

```cpp
[DefaultUninstall]
DelFiles   = ExampleFileSystem.DriverFiles
DelReg     = ExampleFileSystem.DelRegistry
```

[**DelReg**](../install/inf-delreg-directive.md)指令是指一个或多个 INF 写入器定义的**DelRegistry**部分，其中包含要从注册表中删除的要卸载的服务的任何信息。

### <a name="defaultuninstallservices-section-optional"></a>DefaultUninstall 节 (可选) 

**DefaultUninstall**部分是可选的，但如果你的驱动程序可以卸载，则建议使用。 它包含用于删除文件系统驱动程序服务的 [**DelService**](../install/inf-delservice-directive.md) 指令。

在下面的代码示例中， [**DelService**](../install/inf-delservice-directive.md) 指令从操作系统中删除文件系统驱动程序的服务。

```cpp
[DefaultUninstall.Services]
DelService = %ServiceName%,0x200
```

> [!NOTE]
> [**DelService**](../install/inf-delservice-directive.md)指令应始终将 0x200 SPSVCINST_STOPSERVICE (指定) 标记，以在删除之前停止服务。

> [!NOTE]
> 某些类的文件系统产品无法完全卸载。 在这种情况下，只需卸载可以卸载的产品组件，并将产品的组件安装在不能卸载的组件上即可。 此类产品的一个示例是 Microsoft 单实例存储 (SIS) 功能。

### <a name="strings-section-required"></a> (必需的字符串部分) 

[**字符串**](../install/inf-strings-section.md)部分定义了在 INF 文件中使用的每个% strkey% 令牌。

例如，文件系统驱动程序在其 INF 文件中定义以下字符串。

```cpp
[Strings]
Msft        = "Microsoft Corporation"
ServiceDesc = "Example File System Driver"
ServiceName = "ExampleFileSystem"
ParameterPath = "SYSTEM\CurrentControlSet\Services\ExampleFileSystem\Parameters"
Disk1       = "Example File System Driver CD"
```

可以通过创建其他特定于区域设置的 **字符串**来创建单个国际 INF 文件。INF 文件中的*LanguageID* 部分。 有关国际 INF 文件的详细信息，请参阅 [创建国际 Inf 文件](../install/creating-international-inf-files.md)。