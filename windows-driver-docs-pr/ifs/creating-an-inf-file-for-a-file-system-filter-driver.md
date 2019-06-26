---
title: 为文件系统筛选器驱动程序创建 INF 文件
description: 为文件系统筛选器驱动程序创建 INF 文件
ms.assetid: 1e8d0e59-eabd-4bdb-9675-e693a0b364ca
keywords:
- INF 文件 WDK 文件系统中，创建
- SetupAPI WDK 文件系统
- 字符串部分 WDK 文件系统
- DefaultUninstall 部分 WDK 文件系统
- ServiceInstall 部分 WDK 文件系统
- DefaultInstall 部分 WDK 文件系统
- SourceDisksNames 部分 WDK 文件系统
- DestinationDirs 部分 WDK 文件系统
- 版本部分 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 782765223b9c432975dc73816249ca55689455c6
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393502"
---
# <a name="creating-an-inf-file-for-a-file-system-filter-driver"></a>为文件系统筛选器驱动程序创建 INF 文件


## <span id="ddk_creating_an_inf_file_for_a_file_system_filter_driver_if"></span><span id="DDK_CREATING_AN_INF_FILE_FOR_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


Windows 安装程序和设备安装程序服务，总称为[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)，提供控制 Windows 安装程序和驱动程序安装的函数。 安装过程由 INF 文件控制。

文件系统筛选器驱动程序的 INF 文件提供了用于安装驱动程序安装程序 Api 的说明。 INF 文件是文本文件，指定必须存在驱动程序才能运行和的源和目标目录的驱动程序文件的文件。 INF 文件还包含安装程序 Api 将存储在注册表的驱动程序配置信息，如驱动程序的启动类型并加载顺序组。

有关 INF 文件和创建方式的详细信息，请参阅[创建一个 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)并[INF 文件的部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。 有关签名的驱动程序的常规信息，请参阅[驱动程序签名](https://docs.microsoft.com/windows-hardware/drivers/install/driver-signing)。

可以创建一个 INF 文件在多个版本的 Windows 操作系统上安装的驱动程序。 有关创建此类的 INF 文件的详细信息，请参阅[创建多个平台和操作系统的 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)并[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

从 64 位版本的 Windows Vista 中，所有内核模式组件，包括非 PnP （插） 驱动程序，如文件系统驱动程序 （文件系统、 旧筛选器，以及微筛选器驱动程序），必须进行签名以加载和执行。 对于这些版本的 Windows 操作系统中，以下列表包含与文件系统筛选器驱动程序相关的信息。

-   对于非 PnP 驱动程序，包括文件系统驱动程序的 INF 文件不需要包含\[制造商\]或\[模型\]部分。

-   [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)命令行工具，位于\\bin\\SelfSign WDK 安装目录，目录可用于直接"嵌入符号"驱动程序 SYS可执行文件。 出于性能原因，引导启动驱动程序必须包含嵌入式的签名。

-   给定的 INF 文件，请[ **Inf2Cat** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/inf2cat)命令行工具可用于创建驱动程序包的目录 (.cat) 文件。 仅目录文件可以接收[WHQL](https://go.microsoft.com/fwlink/p/?linkid=8705)徽标签名。

-   使用管理员权限，仍可与 Windows Vista 一起启动的基于 x64 的系统上安装未签名的驱动程序。 但是，该驱动程序将无法加载 （并因此执行） 因为它是无符号。

-   关于驾驶签名过程的详细信息，包括推动签名过程对于 64 位版本的 Windows Vista 中，请参阅[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

-   所有内核模式组件，包括自定义内核模式开发工具，必须进行都签名。 有关详细信息，请参阅[签名驱动程序开发和测试 （Windows Vista 和更高版本） 期间](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-during-development-and-test--windows-vista-and-later-)。

若要从注册表中读取信息，或启动用户模式应用程序不能使用 INF 文件。

创建 INF 文件之后，通常将为你安装的应用程序编写的源代码。 在安装应用程序调用用户模式下安装程序函数来访问 INF 文件中的信息和执行安装操作。

要构建自己的筛选器驱动程序 INF 文件，请作为模板的示例文件系统筛选器驱动程序使用 INF 文件。 可以使用[ChkINF](https://docs.microsoft.com/windows-hardware/drivers/devtest/chkinf)工具来检查您的 INF 文件的语法。

文件系统筛选器驱动程序的 INF 文件通常包含以下各节。

-   版本 （必需）

-   DestinationDirs （可选但建议使用）

-   SourceDisksNames （必需）

-   SourceDisksFiles （必需）

-   DefaultInstall （必需）

-   DefaultInstall.Services （必需）

-   ServiceInstall （必需）

-   DefaultUninstall （可选）

-   DefaultUninstall.Services （可选）

-   字符串 （必需）

### <a name="span-idversionsectionrequiredspanspan-idversionsectionrequiredspanspan-idversionsectionrequiredspanversion-section-required"></a><span id="Version_Section__required_"></span><span id="version_section__required_"></span><span id="VERSION_SECTION__REQUIRED_"></span>版本部分 （必需）

[**版本**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)节指定由筛选器的类型的类和 GUID，如下面的代码示例中所示。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = "ActivityMonitor"
ClassGuid   = {b86dff51-a31e-4bac-b3cf-e8cfe75c9fc2}
Provider    = %Msft%
DriverVer   = 08/28/2000,1.0.0.1
CatalogFile = 
```

下表显示的值应该在中指定文件系统筛选器驱动程序[**版本**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)部分。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条目</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>签名</strong></p></td>
<td align="left"><p>"$WINDOWS NT $"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>类</strong></p></td>
<td align="left"><p>请参阅<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">文件系统筛选器驱动程序类和类 Guid</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClassGuid</strong></p></td>
<td align="left"><p>请参阅<a href="file-system-filter-driver-classes-and-class-guids.md" data-raw-source="[File System Filter Driver Classes and Class GUIDs](file-system-filter-driver-classes-and-class-guids.md)">文件系统筛选器驱动程序类和类 Guid</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>提供程序</strong></p></td>
<td align="left"><p>在您自己的 INF 文件，应指定 Microsoft 以外的提供程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>DriverVer</strong></p></td>
<td align="left"><p>请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)"> <strong>INF DriverVer 指令</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CatalogFile</strong></p></td>
<td align="left"><p>将此项留空。 将来，它将包含签名的驱动程序 WHQL 提供目录文件的名称。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspanspan-iddestinationdirssectionoptionalbutrecommendedspandestinationdirs-section-optional-but-recommended"></a><span id="DestinationDirs_Section__optional_but_recommended_"></span><span id="destinationdirs_section__optional_but_recommended_"></span><span id="DESTINATIONDIRS_SECTION__OPTIONAL_BUT_RECOMMENDED_"></span>（可选但建议这样做） DestinationDirs 部分

[ **DestinationDirs** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)部分指定将在其中复制筛选器驱动程序和应用程序文件的目录。

在本部分中并在**ServiceInstall**部分中，您可以通过使用系统定义的数字值指定的已知的系统目录。 有关这些值的列表，请参阅[ **INF DestinationDirs 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)。 在下面的代码示例中，值"12"引用的驱动程序目录 (%windir%\\system32\\驱动程序)，和的值"10"是指 Windows 目录 （%windir%)。

```cpp
[DestinationDirs]
DefaultDestDir             = 12
MyLegacyFilter.DriverFiles = 12
MyLegacyFilter.UserFiles   = 10,MyLegacyFilter
```

### <a name="span-idsourcedisksnamessectionrequiredspanspan-idsourcedisksnamessectionrequiredspanspan-idsourcedisksnamessectionrequiredspansourcedisksnames-section-required"></a><span id="SourceDisksNames_Section__required_"></span><span id="sourcedisksnames_section__required_"></span><span id="SOURCEDISKSNAMES_SECTION__REQUIRED_"></span>SourceDisksNames 部分 （必需）

[ **SourceDisksNames** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)部分指定要使用的分发媒体。

在下面的代码示例中， [ **SourceDisksNames** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)部分列出了单个分发媒体。 媒体的唯一标识符为 1。 由 %disk1%令牌中，定义中指定的介质的名称[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) INF 文件部分。

```cpp
[SourceDisksNames]
1 = %Disk1%
```

### <a name="span-idsourcedisksfilessectionrequiredspanspan-idsourcedisksfilessectionrequiredspanspan-idsourcedisksfilessectionrequiredspansourcedisksfiles-section-required"></a><span id="SourceDisksFiles_Section__required_"></span><span id="sourcedisksfiles_section__required_"></span><span id="SOURCEDISKSFILES_SECTION__REQUIRED_"></span>SourceDisksFiles 部分 （必需）

[ **SourceDisksFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)部分指定的位置和要复制的文件的名称。

在下面的代码示例中， [ **SourceDisksFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)部分列出的驱动程序复制的文件，并指定可以其唯一标识符为 1 （这在介质上找到的文件在定义标识符[ **SourceDisksNames** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section) INF 文件部分。)

```cpp
[SourceDisksFiles]
myLegacyFilter.exe = 1
myLegacyFilter.sys = 1
```

### <a name="span-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspanspan-iddefaultinstallsectionrequiredspandefaultinstall-section-required"></a><span id="DefaultInstall_Section__required_"></span><span id="defaultinstall_section__required_"></span><span id="DEFAULTINSTALL_SECTION__REQUIRED_"></span>DefaultInstall 部分 （必需）

在中[ **DefaultInstall** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)部分中， [ **CopyFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令将文件系统筛选器驱动程序的驱动程序文件复制和用户应用程序文件中指定的目标[ **DestinationDirs** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)部分。

**请注意**   [ **CopyFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令应引用编录文件或该 INF 文件，然后重试。安装程序 Api 将自动复制这些文件。

 

可以创建一个 INF 文件在多个版本的 Windows 操作系统上安装的驱动程序。 通过创建其他来创建此类型的 INF 文件[ **DefaultInstall**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)， [ **DefaultInstall.Services**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)， **DefaultUninstall**，并**DefaultUninstall.Services**的部分，了解每个操作系统版本。 每个部分都标有*修饰*（如.ntx86、.ntia64 或.nt），指定它所应用于的操作系统版本。 有关创建此类型的 INF 文件的详细信息，请参阅[创建多个平台和操作系统的 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-inf-files-for-multiple-platforms-and-operating-systems)。

在下面的代码示例中， [ **CopyFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令将复制的 INF 文件在 MyLegacyFilter.DriverFiles 和 MyLegacyFilter.UserFiles 部分中列出的文件。

```cpp
[DefaultInstall]
OptionDesc = %MyLegacyFilterServiceDesc%
CopyFiles = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
```

### <a name="span-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspanspan-iddefaultinstallservicessectionrequiredspandefaultinstallservices-section-required"></a><span id="DefaultInstall.Services_Section__required_"></span><span id="defaultinstall.services_section__required_"></span><span id="DEFAULTINSTALL.SERVICES_SECTION__REQUIRED_"></span>DefaultInstall.Services 部分 （必需）

[ **DefaultInstall.Services** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)部分包含[ **AddService** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令，用于控制如何以及何时的服务加载特定的驱动程序。

在下面的代码示例中， [ **AddService** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令将 MyLegacyFilter 服务添加到操作系统。 %Mylegacyfilterservicename%令牌包含在中定义的服务名称字符串[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) INF 文件部分。 MyLegacyFilter.Service 是示例驱动程序的名称**ServiceInstall**部分。

```cpp
[DefaultInstall.Services]
AddService = %MyLegacyFilterServiceName%,,MyLegacyFilter.Service
```

### <a name="span-idddkserviceinstallsectionifspanspan-idddkserviceinstallsectionifspanserviceinstall-section-required"></a><span id="ddk_serviceinstall_section_if"></span><span id="DDK_SERVICEINSTALL_SECTION_IF"></span>ServiceInstall 部分 （必需）

**ServiceInstall**部分添加子项或值到注册表名称，并设置值。 名称**ServiceInstall**部分必须出现在[ **AddService** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令[ **DefaultInstall.Services**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)部分。

下面的代码示例演示**ServiceInstall** MyLegacyFilter 示例驱动程序的部分。

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

**DisplayName**条目指定服务的名称。 在中定义的 %mylegacyfilterservicename%令牌在前面的示例中，指定服务名称字符串[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) INF 文件部分。

**说明**项指定一个字符串，描述该服务。 在上述示例中，此字符串指定中定义的 %mylegacyfilterservicedesc%令牌[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) INF 文件部分。

**ServiceBinary**条目指定服务的可执行文件的路径。 在前面的示例中，值 12 引用的驱动程序目录 (%windir%\\system32\\驱动程序)。

**ServiceType**条目指定的服务的类型。 下表列出了可能的值为**ServiceType**及其对应的服务类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
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
<td align="left"><p>SERVICE_WIN32_SHARE_PROCESS （共享一个进程的 Win32 服务）</p></td>
</tr>
</tbody>
</table>

 

**ServiceType**条目应始终设置为服务\_文件\_系统\_文件系统筛选器驱动程序的驱动程序。

**StartType**条目指定在启动服务。 下表列出了可能的值为**StartType**和及其相应的启动类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
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

 

有关详细的说明这些入门类型，请参阅[确定当驱动程序加载的内容](what-determines-when-a-driver-is-loaded.md)。

如果驱动程序的启动类型是服务\_引导\_开始 （即，该驱动程序是引导启动驱动程序），您应确保**LoadOrderGroup**条目是适用于你的筛选器的类型开发。 若要选择加载顺序组，请参阅[文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。 此外，从基于 x64 的 Windows Vista 系统，引导启动驱动程序的二进制图像文件必须包含嵌入式的签名。 此要求确保优化系统的启动性能。 有关详细信息，请参阅[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=79445)。

有关如何信息**StartType**并**LoadOrderGroup**条目确定加载驱动程序时，请参阅[确定当驱动程序加载的内容](what-determines-when-a-driver-is-loaded.md)。

**ErrorControl**条目指定服务在系统启动期间启动失败时要采取的操作。 下表列出了可能的值为**ErrorControl**和控制值及其对应的错误。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000000</p></td>
<td align="left"><p>SERVICE_ERROR_IGNORE （记录错误并继续系统启动）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>SERVICE_ERROR_NORMAL （记录错误、 向用户显示一条消息并继续系统启动。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>SERVICE_ERROR_SEVERE (切换到注册表的 LastKnownGood 控件集和继续系统启动。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000003</p></td>
<td align="left"><p>SERVICE_ERROR_CRITICAL （如果系统启动时未使用注册表的 LastKnownGood 控件集，切换到 LastKnownGood，然后重试。 如果启动仍失败，运行错误检查例程。 启动系统所需的驱动程序应指定此值在其 INF 文件中。）</p></td>
</tr>
</tbody>
</table>

 

**LoadOrderGroup**条目应设置为适用于类型的文件系统筛选器驱动程序开发的加载顺序组。 若要选择加载顺序组，请参阅[文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。

[ **AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)指的是编写器定义的一个或多个 INF **AddRegistry**包含要存储在注册表中的任何信息的部分新已安装的服务。

**请注意**  如果 INF 文件还将使用初始安装中包含的项完成后升级驱动程序**AddRegistry**部分应指定 0x00000002 (FLG\_ADDREG\_NOCLOBBER) 标志。 指定此标志将保留在 HKLM 注册表项\\CurrentControlSet\\服务时安装后续文件。 例如：

 

```cpp
[ExampleFileSystem.AddRegistry]
HKR,Parameters,ExampleParameter,0x00010003,1
```

### <a name="span-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspanspan-iddefaultuninstallsectionoptionalspandefaultuninstall-section-optional"></a><span id="DefaultUninstall_Section__optional_"></span><span id="defaultuninstall_section__optional_"></span><span id="DEFAULTUNINSTALL_SECTION__OPTIONAL_"></span>DefaultUninstall 部分 （可选）

**DefaultUninstall**部分是可选的但建议执行，如果可以卸载您的驱动程序。 它包含[ **DelFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)并[ **DelReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)指令以删除文件和注册表项。

在下面的代码示例中， [ **DelFiles** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delfiles-directive)指令将删除的驱动程序的 INF 文件在 MyLegacyFilter.DriverFiles 和 MyLegacyFilter.UserFiles 部分中列出的文件：

```cpp
[DefaultUninstall]
DelFiles   = MyLegacyFilter.DriverFiles, MyLegacyFilter.UserFiles
DelReg     = MyLegacyFilter.DelRegistry
```

[ **DelReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delreg-directive)指令是指编写器定义的一个或多个 INF **DelRegistry**部分，其中包含要从服务注册表中删除任何信息正在卸载的。

### <a name="span-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspanspan-iddefaultuninstallservicessectionoptionalspandefaultuninstallservices-section-optional"></a><span id="DefaultUninstall.Services_Section__optional_"></span><span id="defaultuninstall.services_section__optional_"></span><span id="DEFAULTUNINSTALL.SERVICES_SECTION__OPTIONAL_"></span>DefaultUninstall.Services 部分 （可选）

**DefaultUninstall.Services**部分是可选的但建议执行，如果可以卸载您的驱动程序。 它包含[ **DelService** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)指令以删除的文件系统筛选器驱动程序的服务。

在下面的代码示例中， [ **DelService** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)指令会从操作系统删除 MyLegacyFilter 服务。

```cpp
[DefaultUninstall.Services]
DelService = MyLegacyFilter,0x200
```

**请注意**   [ **DelService** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-delservice-directive)指令应始终指定 0x200 (SPSVCINST\_STOPSERVICE) 标志，用于在被删除之前停止服务。

 

### <a name="span-idstringssectionrequiredspanspan-idstringssectionrequiredspanspan-idstringssectionrequiredspanstrings-section-required"></a><span id="Strings_Section__required_"></span><span id="strings_section__required_"></span><span id="STRINGS_SECTION__REQUIRED_"></span>（必需） 的字符串部分

[**字符串**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)部分定义使用 INF 文件中的每个 %strkey%标记，如下面的示例中所示。

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

可以通过创建其他特定于区域设置创建一个国际 INF 文件[**字符串。** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) *LanguageID* INF 文件中的部分。 有关国际 INF 文件的详细信息，请参阅[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

 

 




