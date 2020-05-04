---
title: 为文件系统筛选器驱动程序创建 INF 文件
description: 为文件系统筛选器驱动程序创建 INF 文件
ms.assetid: 1e8d0e59-eabd-4bdb-9675-e693a0b364ca
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
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e059b72e9e6185ab2278ca662fa42d28afddbf28
ms.sourcegitcommit: b3bcd94c24b19b4c76c3b49672e237af03b3a7f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82173543"
---
# <a name="creating-an-inf-file-for-a-file-system-filter-driver"></a>为文件系统筛选器驱动程序创建 INF 文件


## <span id="ddk_creating_an_inf_file_for_a_file_system_filter_driver_if"></span><span id="DDK_CREATING_AN_INF_FILE_FOR_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


Windows 安装程序和设备安装程序服务（统称为[setupapi.log](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)）提供控制 Windows 安装程序和驱动程序安装的功能。 安装过程由 INF 文件控制。

文件系统筛选器驱动程序的 INF 文件提供 Setupapi.log 用于安装驱动程序的说明。 INF 文件是一个文本文件，该文件指定要运行的驱动程序必须存在的文件，以及驱动程序文件的源和目标目录。 INF 文件还包含 Setupapi.log 存储在注册表中的驱动程序配置信息，如驱动程序的启动类型和加载顺序组。

有关 INF 文件及其创建方式的详细信息，请参阅[创建 Inf 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)和[inf 文件部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。 有关签名驱动程序的常规信息，请参阅[驱动程序签名](https://docs.microsoft.com/windows-hardware/drivers/install/driver-signing)。

你可以创建一个 INF 文件，用于在多个版本的 Windows 操作系统上安装驱动程序。 有关创建此类 INF 文件的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)和[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

从64位版本的 Windows Vista 开始，所有内核模式组件（即插即用包括文件系统驱动程序（文件系统、旧筛选器和微筛选器驱动程序））都必须进行签名，以便加载和执行。 对于这些版本的 Windows 操作系统，下表包含与文件系统筛选器驱动程序相关的信息。

-   非 PnP 驱动程序的 INF 文件（包括文件系统驱动程序）不需要\[包含制造商\]或\[型号\]部分。

-   位于[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool) WDK 安装目录的\\bin\\SelfSign 目录中的 SignTool 命令行工具可用于直接 "嵌入签名" 驱动程序的可执行文件。 出于性能方面的考虑，启动驱动程序必须包含一个嵌入签名。

-   给定一个 INF 文件后，可以使用[**Inf2Cat**](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)命令行工具为驱动程序包创建目录（.cat）文件。 只有目录文件才能接收[WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)徽标签名。

-   使用管理员权限时，仍可以在从 Windows Vista 开始的基于 x64 的系统上安装未签名的驱动程序。 但是，驱动程序将无法加载（因而执行），因为它是无符号的。

-   有关驱动签名过程的详细信息，包括适用于64位版本的 Windows Vista 的驱动签名过程，请参阅[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

-   所有内核模式组件（包括自定义内核模式开发工具）都必须经过签名。 有关详细信息，请参阅[在开发和测试期间对驱动程序进行签名（Windows Vista 和更高版本）](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-during-development-and-test--windows-vista-and-later-)。

INF 文件不能用于从注册表读取信息或启动用户模式应用程序。

创建 INF 文件后，通常会为安装应用程序编写源代码。 安装应用程序调用用户模式安装程序功能来访问 INF 文件中的信息并执行安装操作。

若要构造自己的筛选器驱动程序 INF 文件，请使用示例文件系统筛选器驱动程序的 INF 文件作为模板。 可以使用[InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)工具来检查 INF 文件的语法。

文件系统筛选器驱动程序的 INF 文件通常包含以下各节。

-   版本（必需）

-   DestinationDirs （可选，但建议使用）

-   SourceDisksNames （必需）

-   SourceDisksFiles （必需）

-   DefaultInstall （必需）

-   DefaultInstall （必需）

-   ServiceInstall （必需）

-   DefaultUninstall （可选）

-   DefaultUninstall （可选）

-   字符串（必需）

### <a name="span-idversion_section__required_spanspan-idversion_section__required_spanspan-idversion_section__required_spanversion-section-required"></a><span id="Version_Section__required_"></span><span id="version_section__required_"></span><span id="VERSION_SECTION__REQUIRED_"></span>版本部分（必需）

[**版本**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)部分指定由筛选器类型确定的类和 GUID，如下面的代码示例中所示。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 08/28/2000,1.0.0.1
CatalogFile = 
```

下表显示文件系统筛选器驱动程序在 "[**版本**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)" 部分中应指定的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条目</th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>信号</strong></p></td>
<td align="left"><p>"$WINDOWS NT $"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>类</strong></p></td>
<td align="left"><p>请参阅<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">文件系统筛选器驱动程序类和类 guid</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClassGuid</strong></p></td>
<td align="left"><p>请参阅<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">文件系统筛选器驱动程序类和类 guid</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>提供程序</strong></p></td>
<td align="left"><p>在你自己的 INF 文件中，你应该指定除 Microsoft 之外的提供程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DriverVer</strong></p></td>
<td align="left"><p>请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)"><strong>INF DriverVer 指令</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CatalogFile</strong></p></td>
<td align="left"><p>将此项留空。 将来，它将包含已签名驱动程序的 WHQL 提供的编录文件的名称。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddestinationdirs_section__optional_but_recommended_spanspan-iddestinationdirs_section__optional_but_recommended_spanspan-iddestinationdirs_section__optional_but_recommended_spandestinationdirs-section-optional-but-recommended"></a><span id="DestinationDirs_Section__optional_but_recommended_"></span><span id="destinationdirs_section__optional_but_recommended_"></span><span id="DESTINATIONDIRS_SECTION__OPTIONAL_BUT_RECOMMENDED_"></span>DestinationDirs 节（可选，但建议使用）

[**DestinationDirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)节指定将在其中复制筛选器驱动程序和应用程序文件的目录。

在此部分和**ServiceInstall**节中，你可以通过使用系统定义的数值来指定众所周知的系统目录。 有关这些值的列表，请参阅[**INF DestinationDirs 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)。 在下面的代码示例中，值 "12" 指驱动程序目录（% windir%\\system32\\驱动程序），值 "10" 指的是 Windows 目录（% windir%）。

```cpp
[DestinationDirs]
DefaultDestDir             = 12
MyLegacyFilter.DriverFiles = 12
MyLegacyFilter.UserFiles   = 10,MyLegacyFilter
```

### <a name="span-idsourcedisksnames_section__required_spanspan-idsourcedisksnames_section__required_spanspan-idsourcedisksnames_section__required_spansourcedisksnames-section-required"></a><span id="SourceDisksNames_Section__required_"></span><span id="sourcedisksnames_section__required_"></span><span id="SOURCEDISKSNAMES_SECTION__REQUIRED_"></span>SourceDisksNames 部分（必需）

[**SourceDisksNames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)部分指定要使用的分发媒体。

在下面的代码示例中， [**SourceDisksNames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)部分列出了单个分发媒体。 媒体的唯一标识符是1。 媒体的名称由% Disk1% 令牌指定，该令牌在 INF 文件的[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)部分中定义。

```cpp
[SourceDisksNames]
1 = %Disk1%
```

### <a name="span-idsourcedisksfiles_section__required_spanspan-idsourcedisksfiles_section__required_spanspan-idsourcedisksfiles_section__required_spansourcedisksfiles-section-required"></a><span id="SourceDisksFiles_Section__required_"></span><span id="sourcedisksfiles_section__required_"></span><span id="SOURCEDISKSFILES_SECTION__REQUIRED_"></span>SourceDisksFiles 部分（必需）

[**SourceDisksFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)部分指定要复制的文件的位置和名称。

在下面的代码示例中， [**SourceDisksFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)部分列出要为驱动程序复制的文件，并指定文件可以在其唯一标识符为1的媒体上找到（此标识符是在 INF 文件的[**SourceDisksNames**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)部分定义的。）

```cpp
[SourceDisksFiles]
myLegacyFilter.exe = 1
myLegacyFilter.sys = 1
```

### <a name="span-iddefaultinstall_section__required_spanspan-iddefaultinstall_section__required_spanspan-iddefaultinstall_section__required_spandefaultinstall-section-required"></a><span id="DefaultInstall_Section__required_"></span><span id="defaultinstall_section__required_"></span><span id="DEFAULTINSTALL_SECTION__REQUIRED_"></span>DefaultInstall 部分（必需）

在[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)节中， [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令将文件系统筛选器驱动程序的驱动程序文件和用户应用程序文件复制到[**DestinationDirs**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)节中指定的目标。

**请注意**  ， [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令不应引用目录文件或 INF 文件本身;Setupapi.log 会自动复制这些文件。

 

你可以创建一个 INF 文件，用于在多个版本的 Windows 操作系统上安装驱动程序。 通过为每个操作系统版本创建附加的[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)、 [**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)、 **DefaultUninstall**和**DefaultUninstall**节来创建这种类型的 INF 文件。 每个部分都带有一个*修饰*（例如，. ntx86、. ntia64 或 nt）标记，该修饰指定应用的操作系统版本。 有关创建此类 INF 文件的详细信息，请参阅[为多个平台和操作系统创建 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)。

在下面的代码示例中， [**CopyFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令复制 INF 文件的 MyLegacyFilter 和 MyLegacyFilter 部分中列出的文件。

```cpp
[DefaultInstall]
OptionDesc = %MyLegacyFilterServiceDesc%
CopyFiles = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
```

### <a name="span-iddefaultinstallservices_section__required_spanspan-iddefaultinstallservices_section__required_spanspan-iddefaultinstallservices_section__required_spandefaultinstallservices-section-required"></a><span id="DefaultInstall.Services_Section__required_"></span><span id="defaultinstall.services_section__required_"></span><span id="DEFAULTINSTALL.SERVICES_SECTION__REQUIRED_"></span>DefaultInstall 部分（必需）

[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)部分包含的[**AddService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令控制如何以及何时加载特定驱动程序的服务。

在下面的代码示例中， [**AddService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令将 MyLegacyFilter 服务添加到操作系统。 % MyLegacyFilterServiceName% 令牌包含在 INF 文件的[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)部分中定义的服务名称字符串。 MyLegacyFilter 是示例驱动程序的**ServiceInstall**节的名称。

```cpp
[DefaultInstall.Services]
AddService = %MyLegacyFilterServiceName%,,MyLegacyFilter.Service
```

### <a name="span-idddk_serviceinstall_section_ifspanspan-idddk_serviceinstall_section_ifspanserviceinstall-section-required"></a><span id="ddk_serviceinstall_section_if"></span><span id="DDK_SERVICEINSTALL_SECTION_IF"></span>ServiceInstall 部分（必需）

**ServiceInstall**节将子项或值名称添加到注册表中，并设置值。 **ServiceInstall**部分的名称必须出现在[**DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)部分的[**AddService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令中。

下面的代码示例演示了 MyLegacyFilter 示例驱动程序的**ServiceInstall**部分。

```cpp
[MyLegacyFilter.Service]
DisplayName    = %MyLegacyFilterServiceName%
Description    = %MyLegacyFilterServiceDesc%
ServiceBinary  = %12%\myLegacyFilter.sys
ServiceType    = 2 ;    SERVICE_FILE_SYSTEM_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL
LoadOrderGroup = "FSFilter Activity Monitor"
AddReg         = MyLegacyFilter.AddRegistry
```

**DisplayName**项指定服务的名称。 在前面的示例中，服务名称字符串由% MyLegacyFilterServiceName% 令牌指定，该令牌在 INF 文件的[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)部分中定义。

**Description**条目指定描述服务的字符串。 在前面的示例中，此字符串由% MyLegacyFilterServiceDesc% 令牌指定，该令牌在 INF 文件的[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)部分中定义。

**ServiceBinary**项指定服务的可执行文件的路径。 在前面的示例中，值12是指驱动程序目录（% windir%\\system32\\驱动程序）。

**ServiceType**条目指定服务的类型。 下表列出了**ServiceType**的可能值及其相应的服务类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_KERNEL_DRIVER （设备驱动程序服务）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_FILE_SYSTEM_DRIVER （文件系统或文件系统筛选器驱动程序服务）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>SERVICE_WIN32_OWN_PROCESS （在其自己的进程中运行的 Microsoft Win32 服务）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>SERVICE_WIN32_SHARE_PROCESS （共享进程的 Win32 服务）</p></td>
</tr>
</tbody>
</table>

 

对于**ServiceType**文件系统筛选器驱动程序，ServiceType\_条目\_应\_始终设置为 "服务文件系统驱动程序"。

**StartType**项指定启动服务的时间。 下表列出了**StartType**的可能值及其相应的启动类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_BOOT_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_SYSTEM_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_AUTO_START</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_DEMAND_START</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000004</p></td>
<td align="left"><p>SERVICE_DISABLED</p></td>
</tr>
</tbody>
</table>

 

有关这些启动类型的详细说明，请参阅[确定何时加载驱动程序的内容](what-determines-when-a-driver-is-loaded.md)。

如果驱动程序的启动类型为 "\_服务\_启动启动" （也就是说，驱动程序是启动启动驱动程序），则还应确保**LoadOrderGroup**条目适用于正在开发的筛选器类型。 若要选择加载顺序组，请参阅[为文件系统筛选器驱动程序加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。 此外，从基于 x64 的 Windows Vista 系统开始，启动驱动程序的二进制图像文件必须包含一个嵌入签名。 此要求可确保系统的最佳启动性能。 有关详细信息，请参阅[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

有关**StartType**和**LoadOrderGroup**条目如何确定何时加载驱动程序的信息，请参阅[确定何时加载驱动程序的内容](what-determines-when-a-driver-is-loaded.md)。

**ErrorControl**项指定在系统启动过程中服务无法启动时要执行的操作。 下表列出了**ErrorControl**的可能值及其相应的错误控制值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_ERROR_IGNORE （记录错误并继续系统启动。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_ERROR_NORMAL （记录错误、向用户显示一条消息，然后继续系统启动。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_ERROR_SEVERE （切换到注册表的 LastKnownGood 控件集，然后继续系统启动。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_ERROR_CRITICAL （如果系统启动未使用注册表的 LastKnownGood 控制集，请切换到 LastKnownGood，然后重试。 如果启动仍然失败，请运行 bug 检查例程。 只有系统启动所需的驱动程序才能在其 INF 文件中指定此值。）</p></td>
</tr>
</tbody>
</table>

 

应将**LoadOrderGroup**项设置为适用于正在开发的文件系统筛选器驱动程序类型的加载顺序组。 若要选择加载顺序组，请参阅[为文件系统筛选器驱动程序加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。

[**AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)是指一个或多个 INF 写入器定义的**AddRegistry**部分，其中包含要存储在注册表中用于新安装的服务的任何信息。

**注意**  如果在初始安装后 INF 文件还将用于升级驱动程序，则**AddRegistry**部分中包含的项应指定0x00000002 （FLG\_ADDREG\_NOCLOBBER）标志。 如果指定此标志，则会在安装\\后续\\文件时保留 HKLM CurrentControlSet Services 中的注册表项。 例如：

 

```cpp
[ExampleFileSystem.AddRegistry]
HKR,Parameters,ExampleParameter,0x00010003,1
```

### <a name="span-iddefaultuninstall_section__optional_spanspan-iddefaultuninstall_section__optional_spanspan-iddefaultuninstall_section__optional_spandefaultuninstall-section-optional"></a><span id="DefaultUninstall_Section__optional_"></span><span id="defaultuninstall_section__optional_"></span><span id="DEFAULTUNINSTALL_SECTION__OPTIONAL_"></span>DefaultUninstall 节（可选）

**DefaultUninstall**节是可选的，但如果你的驱动程序可以卸载，则建议使用。 它包含[**DelFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)和[**DelReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)指令以删除文件和注册表项。

在下面的代码示例中， [**DelFiles**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)指令会删除驱动程序的 INF 文件的 DriverFiles 和 MyLegacyFilter 部分中列出的文件：

```cpp
[DefaultUninstall]
DelFiles   = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
DelReg     = MyLegacyFilter.DelRegistry
```

[**DelReg**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)指令是指一个或多个 INF 写入器定义的**DelRegistry**部分，其中包含要从注册表中删除的要卸载的服务的任何信息。

### <a name="span-iddefaultuninstallservices_section__optional_spanspan-iddefaultuninstallservices_section__optional_spanspan-iddefaultuninstallservices_section__optional_spandefaultuninstallservices-section-optional"></a><span id="DefaultUninstall.Services_Section__optional_"></span><span id="defaultuninstall.services_section__optional_"></span><span id="DEFAULTUNINSTALL.SERVICES_SECTION__OPTIONAL_"></span>DefaultUninstall 节（可选）

**DefaultUninstall**部分是可选的，但如果你的驱动程序可以卸载，则建议使用。 它包含用于删除文件系统筛选器驱动程序服务的[**DelService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)指令。

在下面的代码示例中， [**DelService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)指令从操作系统中删除 MyLegacyFilter 服务。

```cpp
[DefaultUninstall.Services]
DelService = MyLegacyFilter,0x200
```

**请注意**   ， [**DelService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)指令应始终指定0x200 （SPSVCINST\_STOPSERVICE）标志来停止服务，然后再将其删除。

 

### <a name="span-idstrings_section__required_spanspan-idstrings_section__required_spanspan-idstrings_section__required_spanstrings-section-required"></a><span id="Strings_Section__required_"></span><span id="strings_section__required_"></span><span id="STRINGS_SECTION__REQUIRED_"></span>字符串部分（必需）

[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)部分定义了在 INF 文件中使用的每个% strkey% 令牌，如下面的示例中所示。

```cpp
[Strings]
Msft                      = "Microsoft Corporation"
MyLegacyFilterServiceDesc = "MyLegacyFilterFilter Driver"
MyLegacyFilterServiceName = "MyLegacyFilter"
MyLegacyFilterRegistry    = "system\currentcontrolset\services\MyLegacyFilter"
MyLegacyFilterMaxRecords  = "MaxRecords"
MyLegacyFilterMaxNames    = "MaxNames"
MyLegacyFilterDebugFlags  = "DebugFlags"
Disk1                     = "MyLegacyFilter Source Media"
```

可以通过创建其他特定于区域设置的字符串来创建单个国际 INF 文件[**。**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)INF 文件中的*LanguageID*部分。 有关国际 INF 文件的详细信息，请参阅[创建国际 Inf 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

 

 




